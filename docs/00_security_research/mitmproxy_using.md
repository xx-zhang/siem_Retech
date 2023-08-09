# mitmproxy 安装部署
- [自研工具的gitee仓库](https://gitee.com/actanble/mitm_addon)

## DOcker 安装

```bash
docker run --rm -it --net=host \
    --name=mitm \
    -v /etc/localtime:/etc/localtime:ro \
    -v $(pwd)/addons/:/mitm/addons/ \
    registry.cn-beijing.aliyuncs.com/rapid7/mitm:v0 \
    /usr/local/bin/mitmproxy  -k --listen-port 63333  \
    --listen-host 0.0.0.0  \
    -s /root/addons/http_handler.py
```


## 普通使用,单纯代理
> 默认启动; 纯碎是官方的，切记安装证书是 点击 [http://mitm.it/](http://mitm.it/)
```bash
docker run --rm -it --net=host \
    --name=mitm -e LANG=en_US.UTF-8  \
    registry.cn-beijing.aliyuncs.com/rapid7/mitm:v0 \
    /usr/bin/mitmproxy  -k --listen-port 63333  \
    --listen-host 0.0.0.0
```
- [自定义证书](https://docs.mitmproxy.org/stable/concepts-certificates/)

## squid 代理使用过程
- squid 可用；注意修改 `http allow all` 即可。

## 创建以及信任证书（Linux）
```bash 
mkdir certs && cd certs \
openssl req -x509 -nodes -days 365 \
-newkey rsa:2048 \
-subj "/C=CN/ST=HB/L=WH/O=actanble/OU=dev/CN=admin@actanble.onaliyun.com/emailAddress=actanble@gmail.com" \
-keyout $(pwd)/local.key \
-out $(pwd)/local.crt
cat local.key local.crt > local.pem

openssl pkcs12 -export -inkey local.key -in local.pem -out local.p12
```