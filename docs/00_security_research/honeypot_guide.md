# 蜜网教程
- [权威蜜罐大全](https://github.com/paralax/awesome-honeypots)
- [知乎总结](https://zhuanlan.zhihu.com/p/110886405)
- [freebuf蜜罐测评](https://www.freebuf.com/articles/paper/207739.html)

## 代理蜜罐
- [frebuf golang开发代理蜜罐](https://www.freebuf.com/articles/network/202310.html)

## Tpot-ce
- [tpotce部署](https://www.izhuhn.cn/index.php/2019/05/24/%e5%bc%80%e6%ba%90%e8%9c%9c%e7%bd%90t-pot-19-03%e5%ae%89%e8%a3%85%e5%92%8c%e4%bd%bf%e7%94%a8/)

## mhn-现代密网
- [开源蜜罐mhn](https://blog.csdn.net/u012206617/category_9220620.html)

### 蜜网技术研究
- 开始探索蜜网技术。
- [github蜜罐大全](https://github.com/paralax/awesome-honeypots)
- [tpotce部署](https://www.izhuhn.cn/index.php/2019/05/24/%e5%bc%80%e6%ba%90%e8%9c%9c%e7%bd%90t-pot-19-03%e5%ae%89%e8%a3%85%e5%92%8c%e4%bd%bf%e7%94%a8/)
- openflow交换 密网技术;

## opencanary
> 非常适合二次开发的python蜜罐;模拟服务.
- [opencanary](http://pirogue.org/2019/01/15/opencanary_2/#%E8%A7%A6%E5%8F%91%E6%96%B9%E5%BC%8F)

## 模拟漏洞系列.
- [常见漏洞大全](https://github.com/vulhub/vulhub)


## hfish快速开始

```bash
docker run -d --name hfish \
    -p 21:21 \
    -p 22:22 \
    -p 23:23 \
    -p 69:69 \
    -p 3306:3306 \
    -p 5900:5900 \
    -p 6379:6379 \
    -p 8080:8080 \
    -p 8081:8081 \
    -p 8989:8989 \
    -p 9000:9000 \
    -p 9001:9001 \
    -p 9200:9200 \
    -p 11211:11211 \
    --restart=always \
    registry.cn-beijing.aliyuncs.com/rapid7/hfish:v0.0.6

docker run -d --name hfishX \
    --net=host \
    --restart=always \
    registry.cn-beijing.aliyuncs.com/rapid7/hfish:v0.0.6
```

## 日志轮转
- suricata ids模式日志轮转。



## iptables 封禁
```bash

iptables -A INPUT -p tcp --dport 9001 -j DROP
iptables -I INPUT -s 127.0.0.1 -p tcp --dport 9001 -j ACCEPT
```

## certbot 使用
```bash

wget -c -N https://dl.eff.org/certbot-auto && \
    chmod a+x ./certbot-auto && \
    ./certbot-auto --help

./certbot-auto --server \
    https://acme-v02.api.letsencrypt.org/directory -d "kac.fun" -d "*.kac.fun" \
    --manual --preferred-challenges dns-01 certonly
```

## 反制
- [避免踩坑](https://www.freebuf.com/articles/network/116922.html)
- [kippo-ssh](https://github.com/desaster/kippo)
- [内网tips](https://github.com/Ridter/Intranet_Penetration_Tips)
