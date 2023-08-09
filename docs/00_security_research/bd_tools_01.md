# 部门工具概览


## nginx / web中间件

> 另外 bd_waf 也是同理。

### 日志记录请求体
```
# http://nginx.org/en/docs/http/ngx_http_core_module.html#.24request_body
log_format ngxkv 'request_id="$request_id" '
				'time_local="$time_local" '
				'timestamp="$time_iso8601" '
				'server_addr="$server_addr" '
				'host="$host" '
				'server_port="$server_port" '
				'remote_addr="$remote_addr" '
				'remote_user="$remote_user" '
				'remote_user="$remote_user" '
                 'request_time="$request_time" '
                 'request_method="$request_method" '
                 'request_uri="$request_uri" '
                 'uri="$uri" '
                 'server_protocol="$server_protocol" '
                 'http_params="$args" '
                 'http_body="$request_body" '
                 'http_status="$status" '
                 'http_referer="$http_referer" '
                 'http_user_agent="$http_user_agent" '
                 'http_cookie="$http_cookie" '
                 'content_type="$content_type" '
                 'proxy_server="$proxy_protocol_server_addr:$proxy_protocol_server_port" '
                 'proxy_client="$proxy_protocol_addr:$proxy_protocol_port" '
                 'connection="$connection" '
                 'connection_requests_num="$connection_requests" '
                 'http_x_forwarded_for="$http_x_forwarded_for" '
                 'body_bytes_sent="$body_bytes_sent" '
                 'request="$request" '
                 'request_completion="$request_completion" '
                 'upstream_response_time="$upstream_response_time" '
                 'upstream_addr="$upstream_addr"';

```
### server 中的设置

```title='conf/vhosts/default.conf'
upstream webmin {
	server 127.0.0.1:49153;
}

server {

        include custom-error-page.conf;


        listen 0.0.0.0:3380;
        listen [::]:3380;
        server_name  _;

        #index index.jsp index.action index.htm index.html;

        error_page 497 https://$server_name$request_uri;
        #proxy_set_header   Host             $host;
        proxy_set_header Host $host:$server_port;
        proxy_set_header   X-Real-IP        $remote_addr;
        proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
        proxy_set_header   X-Forwarded-Scheme $scheme;
        proxy_next_upstream http_502 http_504 error timeout invalid_header;
        proxy_redirect http:// $scheme://;
        port_in_redirect on;
        proxy_read_timeout 1200;

        proxy_intercept_errors off;
        proxy_hide_header Server;

        # 适配 websocket
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";


         location / {
            access_log var/logs/proxy-host.log ngxkv;
            proxy_pass http://webmin;
            #proxy_cookie_path  /cookie  /;
            #autoindex on;
            #root html;
            #sub_filter 'nginx' 'ngtp.webserver';
            #sub_filter_once off;
        }

    }

#server {
#     listen 0.0.0.0:80;
#     listen [::]:80;
#     server_name *.*.*.*;
#     rewrite ^(.*)$ https://${server_addr}$1 permanent;
#
# }
```

## bd_nids

### 2 适用范围
网络入侵检测系统 NIDS
Ubuntu16+/ centos7 上可以部署使用。 centos7.9 可以使用pfring的配置。

### 术语及定义

## 0x01 入侵检测系统介绍

NIDS 入侵检测系统国标文档
GB／T 20275-2013  信息安全技术 网络入侵检测系统技术要求和测试评价方法

### 1.1.1 Snort的介绍说明

> Snort已发展成为一个具有多平台(Multi-Platform)、实时(Real-Time)流量分析、网络IP数据包(Pocket)记录等特性的强大的网络入侵检测/防御系统(Network Intrusion Detection/Prevention System)，即NIDS/NIPS。
Snort有三种工作模式：嗅探器、数据包记录器、网络入侵检测系统。
Snort入侵检测系统适应多种平台，源代码开放，使用免费，但也有不少缺点。Snort之所以说他是轻量型就是说他的功能还不够完善，比如与其它产品产生联动等方面还有待改进；Snort由各功能插件协同工作，安装复杂，各软件插件有时会因版本等问题影响程序运行；Snort对所有流量的数据根据规则进行匹配，有时会产生很多合法程序的误报。

### 1.1.2 Suricata介绍及使用

> 这是一种IDS引擎，它使用规则集来监控网络流量，并在发生可疑事件时触发警报。 Suricata提供多线程引擎，这意味着它可以以更快的速度和效率执行网络流量分析。
Suricata采用多线程模式处理，多线程任务分为三种模式，Single,Worker,Autofp模式。Suricata的多线程和模块化设计上使其在效率和性能上超过了原有Snort，它将 CPU 密集型的深度包检测工作并行地分配给多个并发任务来完成。这样的并行检测可以充分利用多核硬件的优势来提升入侵检测系统的吞吐量，在数据包的深度检测上效果优越。
Suricata算是加强版的snort，在网络包捕获，多核，硬件加速等性能方面对比snort优势非常明显，同时加强了对应用层（http，ftp等）协议的检测，对比也有比较明显的优势，同时最新版基本兼容snort的规则，少部分规则和snort有不同之处，这个主要是由于增加了对应用层检测而出现的不同。

### 1.1.3 Suricata 部署使用说明。[自己编译]

>部署说明查看另外一篇文档。这里简单说下，依赖的就是libpcap\rust\perl\pcre等一些基础依赖的工具，安装完成后三部曲编译suricata-6.0.2即可。
官方教程  https://redmine.openinfosecfoundation.org/projects/suricata/wiki/Suricata_Installation
Centos7参考 https://www.liangzl.com/get-article-detail-174679.html
Ubuntu/Debian 参考 https://github.com/al0ne/suricata_optimize
Docker 安装参考我准备的压缩包 ids-tools 里面的 `install_suricata`
Centos7下的编译脚本，以及做到了适配linux内核2.9+； 有需要可以和我联系。当然其中核心的地方是规则清洗和相关漏报的威胁检测的规则的补充


## 0x02 使用安装

###  安装引擎 BD_NIDS

当前版本最新是  `bd_nids-v3.0.0.20210915.linux.base.tar.gz`

	默认使用的是 af_packet 抓包，使用的是autofp 也就是流过来后单线程分配到引擎的管道上，如果使用pfring必须是centos7.9 是多线程分担到各个管道，效率更高。

使用

```
tar xf bd_nids-v3.0.0.20210915.linux.base.tar.gz 
cd bd_nids 
sed -i 's/ens160/你的网卡名字/1' nids   // 或者手动修改 IFACE=你的网卡名
./nids start 或者 /bd_nids/nids start 

./nids 还有分析pcap的功能 
/bd_nids  rdpcap  <pcap路径>
```

### 1.2.2安装日志发送工具发送到kafka (可选)

```
tar xf evelog_v3.0.0.20210916.x86.Linux.tar.gz  
evelog &  后台运行即可。
```

> [warning] 需要注意的是配置文件 config.yaml。
Kafka.host 需要修改为我们的kafka_host的配置;
如果不保存到本地就修改 common. save_local 为 false


### 1.2.3 python-sender.py 

```python title=logsender.py

"""
TODO:
    tail 一个日志分拣发送到 syslog 地址。
"""
import os
import sys
import time
import socket


class Tail(object):
    ''' Represents a tail command. '''
    def __init__(self, tailed_file):
        ''' Initiate a Tail instance.
            Check for file validity, assigns callback function to standard out.

            Arguments:
                tailed_file - File to be followed. '''

        self.check_file_validity(tailed_file)
        self.tailed_file = tailed_file
        self.callback = sys.stdout.write

    def follow(self, s=1):
        ''' Do a tail follow. If a callback function is registered it is called with every new line.
        Else printed to standard out.

        Arguments:
            s - Number of seconds to wait between each iteration; Defaults to 1. '''

        with open(self.tailed_file) as file_:
            # Go to the end of file
            file_.seek(0, 2)
            while True:
                curr_position = file_.tell()
                line = file_.readline()
                if not line:
                    file_.seek(curr_position)
                    time.sleep(s)
                else:
                    self.callback(line)

    def register_callback(self, func):
        ''' Overrides default callback function to provided function. '''
        self.callback = func

    def check_file_validity(self, file_):
        ''' Check whether the a given file exists, readable and is a file '''
        if not os.access(file_, os.F_OK):
            raise TailError("File '%s' does not exist" % (file_))
        if not os.access(file_, os.R_OK):
            raise TailError("File '%s' not readable" % (file_))
        if os.path.isdir(file_):
            raise TailError("File '%s' is a directory" % (file_))


class TailError(Exception):
    def __init__(self, msg):
        self.message = msg

    def __str__(self):

        return self.message


# TODO SYSLOG sender

class WelfSender:
    def __init__(self, host: str = '10.7.215.77', port: int = 514, proto: str = "udp"):
        self.host = host
        self.port = port
        self.proto = proto

    def send(self, msg: str):
        if self.proto == "udp":
            sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM) # TODO 无信任连接
        else:
            sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

        sock.connect((self.host, self.port))
        msg2 = (msg + '\n').encode('raw-unicode-escape')
        try:
            sock.sendto(msg2, (self.host, self.port))
        except (AttributeError, socket.error) as e:
            print(e)
            pass
        sock.close()


import argparse
parser = argparse.ArgumentParser(description="ngx bdp 日志发送工具; gen by xx-zhang")
parser.add_argument('-s', '--syslog-host', type=str, help="syslog udp 的HOST (默认 localhost)", default="127.0.0.1")
parser.add_argument('-p', '--syslog-port', type=int, help="syslog udp 的HOST port", default=514)
parser.add_argument('-t', '--syslog-proto', type=str, help="syslog udp 的HOST port", default="udp")
parser.add_argument('-f', '--infile', type=str, default='proxy-host.log', help="日志源选择")
args = parser.parse_args().__dict__.copy()


def send_line(msg: str):
    ''' Prints received text '''
    sender = WelfSender(host=args["syslog_host"], port=args["syslog_port"], proto=args["syslog_proto"])
    sender.send(msg)


def main():
    t = Tail(args["infile"])
    t.register_callback(send_line)
    t.follow(s=3)


if __name__ == '__main__':
    main()

```


## 将suricata日志按照键值对发送到远程
- [参考项目](https://gitee.com/tsc_admin/syslog-ng-python)