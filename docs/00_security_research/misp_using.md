# 威胁情报相关的内容
- misp + thehive + cortex + esalert

##  MISP搭建使用
- 威胁情报部署和使用。


```bash
mkdir -p /docker/certs &&  openssl req -x509 -nodes -days 365 \
-newkey rsa:2048 \
-subj "/C=CN/ST=HB/L=WH/O=actanble/OU=dev/CN=admin@actanble.onaliyun.com/emailAddress=actanble@gmail.com" \
-keyout /docker/certs/misp.key \
-out /docker/certs/misp.crt

docker run -it --rm \
    -v /srv/docker/misp-db:/var/lib/mysql \
    registry.cn-shanghai.aliyuncs.com/rapid7/misp \
    /init-db

docker run -it -d \
    --name=misp \
    -p 443:443 \
    -p 80:80 \
    -p 3306:3306 \
    --restart=always \
    -v /srv/docker/misp-db:/var/lib/mysql \
    -v /docker/certs:/etc/ssl/private \
    registry.cn-shanghai.aliyuncs.com/rapid7/misp
```

## 威胁情报中心
- [awesome-osint](https://github.com/jivoi/awesome-osint)
- MISP/feed [URL](https://10.27.113.2/feeds/add)

## 2020-11-12
- 读取`feed`, 重新上传 `feed`