# frp使用
- [frp工具官网说明教程](https://github.com/fatedier/frp/blob/master/README_zh.md)

## 目标
- 让公网使用本地的网络。
> 本地开放了一个`1080端口`的http代理服务, 将其内网穿透给公网的IP的10080端口.
> 这样公网就可以通过穿透后的10080端口代理自己访问受限制的内网资源。
- 这里我们选择了`frp`内网穿透工具; 因为`frp`是CS架构，所以这里我们可以不用那么拘束。

## 过程 [已完全实现]

1. 具有外网的客户端。这里可以是windows可以是Linux;
### 安装外网代理
- 如果是windows, 使用 ccproxy 工具，并且开放出端口是57321
- 如果是Linux推荐使用socks5、squid等工具。推荐 `danted`

```bash
docker run -d \
    --name sockd \
    --publish 57321:2020 \
    --volume sockd.passwd:/home/danted/conf/sockd.passwd \
    registry.cn-hangzhou.aliyuncs.com/rapid7/dante
```
2. 安装frpc代理
- ccproxy的位置如果是其他的就设置其他的，frpc.ini
- 运行命令 `./frpc -c ./frpc.ini`

```editorconfig  title='frpc.ini'
[common]
server_addr = 10.27.106.221
server_port = 57321

[ccproxy]
type = tcp
local_ip = 10.25.8.188
local_port = 57321
remote_port = 1080
use_encryption = true
use_compression = true
```

3. 在访问受限的机器上安装服务端
- 这里是服务单的内容。
```editorconfig  title='frps.ini'
[common]
bind_port = 57321
#vhost_http_port = 57321 
```
- 运行命令 `./frps -c ./frps.ini`

## 原理解析
- 这里服务端的`57321`只是为了建立一个frp通道的服务，没有其他任何用处。
- 建立服务后将远程的端口转发到本地server的1080端口了。