# 扫描篇 （内网资产扫描）

- [AssetScan- j2ee](https://github.com/JE2Se/AssetScan)


## 添加 openvas（2020-11-5 ）
- [openvas-docker](https://github.com/xx-docker/docker-openvas-based-ub1804)

```bash
docker run -itd --restart=always \
--name=openvas \
-p 9392:9392 \
-v /srv/docker/openvas/var/run:/usr/local/var/run \
registry.cn-hangzhou.aliyuncs.com/rapid7/openvas:v10

docker exec -i openvas < ./update_nvt.sh 
docker exec -i openvas gvmd --create-user=admin002 --password=112233..

docker run -itd --restart=always \
--name=openvas \
-p 9392:9392 \
-v /srv/docker/openvas/var/run:/usr/local/var/run \
registry.cn-hangzhou.aliyuncs.com/rapid7/openvas
```

## masscan
- `sed -i 's/clang/gcc/g' Makefile && make`

```bash
#!/bin/bash

masscan_ver=1.0.5

function error_exit
{
  echo -e "\033[41;30m [ERROR]"$1"\033[0m" 1>&2
  exit 1
}

function install_deps()
{
  yum -y install wget curl make gcc \
    libtiff-devel libffi-devel libjpeg-devel \
    gcc flex bison libpcap-devel;
  yum -y install python3 python3-pip python3-devel ;
  # TODO install nmap
  rpm -vhU https://nmap.org/dist/nmap-7.80-1.x86_64.rpm ;

  wget -c -N https://www.tcpdump.org/release/libpcap-1.9.1.tar.gz && \
    tar xf libpcap-1.9.1.tar.gz && cd libpcap-1.9.1 && ./configure && make && make install
}


function build_masscan()
{
  wget -c -N https://github.com/robertdavidgraham/masscan/archive/${masscan_ver}.tar.gz && \
    tar xf ${masscan_ver}.tar.gz && cd masscan-${masscan_ver} && \
    sed -i 's/clang/gcc/g' Makefile && make
}

build_masscan || error_exit 'install masscan error' ;

```


## 2020-12-1 记录常见中型资产探测解决方案
- [TrackRay 溯光（JAVA）](https://github.com/iSafeBlue/TrackRay)
- [myscan](https://github.com/amcai/myscan)
- [BBscan](https://github.com/lijiejie/BBScan)
- [AssetScan](https://github.com/JE2Se/AssetScan)
- [pentestdb](https://github.com/alpha1e0/pentestdb)
- [web app scanner](https://github.com/m4ll0k/WAScan)
- [Tide资产发现](https://github.com/TideSec/Tide#%E8%B5%84%E4%BA%A7%E5%8F%91%E7%8E%B0)
- [Ladon](https://github.com/k8gege/Ladon)
- [K8tools](https://github.com/k8gege/K8tools)
    - `k8gege.org|k8gege|k8team`
    - [K8tools工具文档](http://k8gege.org/p/72f1fea6.html)
- [scantron - py3/nmap/masscan](https://github.com/rackerlabs/scantron)
- [敏感文件扫描](https://github.com/Mosuan/FileScan/)
- [sN1per](https://github.com/1N3/Sn1per)
- [Vxscan](https://github.com/al0ne/Vxscan)
- [w9scan](https://github.com/w-digital-scanner/w9scan)
- [nmap-scanner](https://github.com/vulnersCom/nmap-vulners/blob/master/vulners.nse)
- [vulscan](https://github.com/scipag/vulscan)

## 打造自己的扫描器，基于celerystalk的想法
- 开始基于上卖弄`vxscan\29scan/assetscan`做一个自研扫描器
- 备份位置 https://192.168.66.211/zhang_xiaoxiang/Xscan/
    - 开发位置 https://github.com/xx-scan/Xscan

## nessus 安装

```
/opt/nessus/sbin/nessuscli fetch --challenge
/opt/nessus/sbin/nessuscli fetch --register-offline nessus/nessus.licence
/opt/nessus/sbin/nessuscli update  all-2.0.tar.gz

find /opt/nessus/lib/nessus/plugins/ -name "*.*" | xargs -i chattr +i {}
chattr -i /opt/nessus/lib/nessus/plugins/plugin_feed_info.inc
cp /opt/nessus/lib/nessus/plugins/plugin_feed_info.inc /opt/nessus/var/nessus/
mkdir -p /opt/nessus/var/nessus/plugins/
cp /opt/nessus/lib/nessus/plugins/plugin_feed_info.inc /opt/nessus/var/nessus/plugins/
chattr +i /opt/nessus/var/nessus/plugin_feed_info.inc 
```

### plugin_feed_info.inc 文件修改
```title='plugin_feed_info.inc'
PLUGIN_SET = "202211110153";
PLUGIN_FEED = "ProfessionalFeed (Direct)";
PLUGIN_FEED_TRANSPORT = "Tenable Network Security Lightning";
```

## 主机存活判断

### ICMP ping
> 可以关闭服务器的ping :echo 1> /proc/sys/net/ipv4/icmp_echo_ignore_all
### TCP connect
> 这种类型就是最传统的扫描技术，程序调用connect()套接口函数连接到目标端口，形成一次完整的TCP三次握手过程，显然能连接得上的目标端口就是开放的。在UNIX下使用这种扫描方式不需要任何权限。还有一个特点，它的扫描速度非常快，可以同时使用多个socket来加快扫描速度，使用一个非阻塞的I/O调用即可以监视多个 socket. 不过由于它不存在隐蔽性，所以不可避免的要被目标主机记录下连接信息和错误信息或者被防护系统拒绝
　　
### TCP SYN
> 这种类型也称为半开放式扫描[half-open scanning] 原理是往目标端口发送一个SYN包，若得到来自目标端口返回的SYN/ACK响应包，则目标端口开放，若得到RST则未开放。在UNIX下执行这种扫描必须拥有ROOT权限。由于它并未建立完整的TCP三次握手过程，很少会有操作系统记录到，因此比起 TCP connect 扫描隐蔽得多，但是若你认为这种扫描方式足够隐秘，那可就错了，有些防火墙将监视TCP SYN扫描，还有一些工具比如synlogger和courtney也能够检测到它。为什么？因为这种秘密扫描方法违反了通例，在网络流量中相当醒目，正是它的刻意追求隐蔽特性留下了狐狸尾巴！
　　
### TCP FIN
> 原理:根据RFC 793文档 程序向一个端口发送FIN，若端口开放则此包将被忽略，否则将返回RST，这个是某些操作系统TCP实现存在的BUG，并不是所有的操作系统都存在这个BUG，所以它的准确率不高，而且此方法往往只能在UNIX上成功地工作，因此这个方法不算特别流行。不过它的好处在于足够隐蔽，如果你判断在使用TCP SYN 扫描时可能暴露自身的话可以一试这种方法。
　　
### TCP reverse ident 扫描
> 1996年 Dave Goldsmith 指出 ,根据RFC1413文档，ident协议允许通过TCP连接得到进程所有者的用户名，即使该进程不是连接发起方。此方法可用于得到FTP所有者信息，以及其他需要的信息等等。
　　
### TCP Xmas Tree 扫描
> 根据RFC 793文档，程序往目标端口发送一个FIN 、URG和PUSH包，若其关闭，应该返回一个RST包
　　
### TCP NULL 扫描
> 根据RFC 793文档，程序发送一个没有任何标志位的TCP包，关着的端口将返回一个RST数据包。
　　
### TCP ACK 扫描
> 这种扫描技术往往用来探测防火墙的类型，根据ACK位的设置情况可以确定该防火墙是简单的包过滤还是状态检测机制的防火墙
　　
### TCP 窗口扫描
> 由于TCP窗口大小报告方式不规则，这种扫描方法可以检测一些类UNIX系统[AIX ， FreeBSD等] 打开的以及是否过滤的端口。
　　
### TCP RPC 扫描
> 这个方式是UNIX系统特有的，可以用于检测和定位远程过程调用[RPC]端口及其相关程序与版本标号。
　　
### UDP ICMP端口不可达扫描
> 此方法是利用UDP本身是无连接的协议，所以一个打开的UDP端口并不会给我们返回任何响应包，不过如果端口关闭，某些系统将返回ICMP_PORT_UNREACH信息。但是由于UDP是不可靠的非面向连接协议，所以这种扫描方法也容易出错，而且还比较慢。
　　
### UDP recvfrom() 和 write() 扫描
> 由于UNIX下非ROOT用户是不可以读到端口不可达信息，所以NMAP提供了这个仅在LINUX下才有效的方式。在LINUX下，若一个UDP端口关闭，则第二次write()操作会失败。并且，当我们调用recvfrom()的时候，若未收到ICMP错误信息，一个非阻塞的UDP 套接字一般返回EAGAIN("Try Again",error=13)，如果收到ICMP的错误信息，套接字返回ECONNREFUSED("Connectionrefused",error=111)。通过这种方式，NMAP将得知目标端口是否打开 [BTW: Fyodor 先生真是伟大！]
　　
### 分片扫描
> 这是其他扫描方式的变形体，可以在发送一个扫描数据包时，将数据包分成许多的IP分片，通过将TCP包头分为几段，放入不同的IP包中，将使得一些包过滤程序难以对其过滤 ，因此这个办法能绕过一些包过滤程序。不过某些程序是不能正确处理这些被人为分割的IP分片，从而导致系统崩溃，这一严重后果将暴露扫描者的行为！
　　
### FTP跳转扫描
>根据RFC 959文档，FTP协议支持代理 [PROXY]， 形象的比喻：我们可以连上提供FTP服务的机器A，然后让A向我们的目标主机B发送数据，当然，一般的FTP主机不支持这个功能。我们若需要扫描B的端口，可以使用PORT命令，声明B的某个端口是开放的，若此端口确实开放，FTP 服务器A将返回150和226信息，否则返回错误信息 :"425 Can't build data connection: Connection refused".这种方式的隐蔽性很不错，在某些条件下也可以突破防火墙进行信息采集，缺点是速度比较慢。
　　
### ICMP 扫射
> 不算是端口扫描，因为ICMP中无抽象的端口概念，这个主要是利用PING指令快速确认一个网段中有多少活跃着的主机。


## RFC 附录
- [rfc1035](https://tools.ietf.org/html/rfc1035)
- [RFC中文查询](http://www.cnpaf.net/)