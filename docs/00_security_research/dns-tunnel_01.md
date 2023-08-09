


- [渗透测试工具库](https://zhuanlan.zhihu.com/p/181396480)
- [DNS-Base](https://zhuanlan.zhihu.com/p/145332177?utm_source=wechat_session&utm_medium=social&utm_oi=845906800787230720)
- [DoH基础](https://zhuanlan.zhihu.com/p/79633364?utm_source=wechat_session&utm_medium=social&utm_oi=845906800787230720)
- [Core-DNS](https://github.com/coredns/coredns)
- [DoH使用和介绍-wiki](https://zh.wikipedia.org/wiki/DNS_over_HTTPS#cite_note-12)
- [dnscat2](https://github.com/iagox86/dnscat2)


## firefox 设置
```
在 Firefox 62 及以上版本中开启 DNS over HTTPS

    在浏览器地址栏输入 about:config 然后打开，并同意警告信息。
    搜索 network.trr
    设置 network.trr.mode 值为2
    在 network.trr.uri 中填入上表中任一服务器，例如：https://1.1.1.1/dns-query
```

## DNS 隧道
- dns2tcp
- dnscat2


## 网关工具

```bash
 iptables -t nat -A POSTROUTING -s 172.21.7.0/24 -j MASQUERADE
```


## [docker 使用代理的方法](https://docs.docker.com/config/daemon/systemd/#httphttps-proxy)

```bash

sudo mkdir -p /etc/systemd/system/docker.service.d && \
echo > /etc/systemd/system/docker.service.d/http-proxy.conf <- EOF
[Service]
Environment="HTTPS_PROXY=http://127.0.0.1:1080/" "NO_PROXY=localhost,127.0.0.1,registry.docker-cn.com,hub-mirror.c.163.com"
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
# systemctl show --property=Environment docker

```

## 端口映射

```bash 
iptables -t nat -A PREROUTING -p tcp -i ens192 --dport 1080 -j DNAT --to 127.0.0.1:1080
iptables -t nat -A POSTROUTING -j MASQUERADE

```

## 升级docker-compose
```bash 

yum -y install python3 python3-devel python3-pip;
pip3 install docker-compose==1.26.2 --index-url https://pypi.tuna.tsinghua.edu.cn/simple
chmod +x /usr/local/bin/docker-compose
ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

## DNS server 
```bash
docker run --ulimit nofile=90000:90000 \
    --name=dnscrypt-server \
     --net=host \
    --restart=unless-stopped \
    -v /etc/dnscrypt-server/keys:/opt/encrypted-dns/etc/keys \
    -v /etc/dnscrypt-server/lists:/opt/encrypted-dns/etc/lists \
     jedisct1/dnscrypt-server init \
    -N wh.vcsa.tsc.com \
    -E 10.27.106.252:443
# docker start dnscrypt-server

docker run --name bind -d --restart=always \
  --publish 53:53/tcp --publish 53:53/udp --publish 10000:10000/tcp \
  --volume /srv/docker/bind:/data \
  sameersbn/bind:9.16.1-20200524
```


##  http被动扫描器(2020-8-14)
- [passive_scan - tornado__5年前](https://github.com/netxfly/passive_scan)
- [burpsuit-passive-scan](https://github.com/c0ny1/passive-scan-client)


## ICMP tunnel

[icmptunnel](https://github.com/DhavalKapil/icmptunnel)

- 上古原始的依赖最小的 `icmptunnel`

ptunnel-0.72

- [ptunnel-using](https://blog.csdn.net/qq_38626043/article/details/104414519)

## [ptunnel-ng](https://github.com/lnslbrty/ptunnel-ng)

```bash

# proxy: Server  
./ptunnel-ng -r127.0.0.1 -R22 -v10 

# Client: 
./ptunnel-ng -p121.41.75.73 -l2222 -r127.0.0.1 -R22 -v10

## Server(proxy)：
sudo ptunnel-ng -r10.0.3.1 -R22
## Client：
sudo ./src/ptunnel-ng -p[Server-IP/NAME] -l2222 -r10.0.3.1 -R22
ssh -R 127.0.0.1:22222 127.0.0.1 -p2222

```

## ids检测
```

{"timestamp":"2021-09-15T14:20:11.143239+0800","flow_id":2135284072036595,"in_iface":"ens32","event_type":"alert","src_ip":"10.27.113.137","src_port":0,"dest_ip":"121.41.75.73","dest_port":0,"proto":"ICMP","icmp_type":8,"icmp_code":0,"alert":{"action":"allowed","gid":1,"signature_id":2024366,"rev":1,"signature":"ET MALWARE OpenSSH in ICMP Payload - Possible Covert Channel","category":"A Network Trojan was detected","severity":1,"metadata":{"affected_product":["Any"],"attack_target":["Client_Endpoint"],"created_at":["2017_06_08"],"deployment":["Perimeter"],"former_category":["TROJAN"],"performance_impact":["Moderate"],"signature_severity":["Major"],"updated_at":["2017_06_08"]}},"flow":{"pkts_toserver":3,"pkts_toclient":4,"bytes_toserver":1276,"bytes_toclient":954,"start":"2021-09-15T14:20:11.112883+0800"},"payload":"3q3A3gAAAAAAAAAAQAAAAgAAAAEAAAQAAAI6PwAABeQKFBdJEBUZA3F5SgQlfn5+H5EAAADxY3VydmUyNTUxOS1zaGEyNTYsY3VydmUyNTUxOS1zaGEyNTZAbGlic3NoLm9yZyxlY2RoLXNoYTItbmlzdHAyNTYsZWNkaC1zaGEyLW5pc3RwMzg0LGVjZGgtc2hhMi1uaXN0cDUyMSxkaWZmaWUtaGVsbG1hbi1ncm91cC1leGNoYW5nZS1zaGEyNTYsZGlmZmllLWhlbGxtYW4tZ3JvdXAxNi1zaGE1MTIsZGlmZmllLWhlbGxtYW4tZ3JvdXAxOC1zaGE1MTIsZGlmZmllLWhlbGxtYW4tZ3JvdXAxNC1zaGEyNTYsZXh0LWluZm8tYwAAAfRlY2RzYS1zaGEyLW5pc3RwMjU2LWNlcnQtdjAxQG9wZW5zc2guY29tLGVjZHNhLXNoYTItbmlzdHAzODQtY2VydC12MDFAb3BlbnNzaC5jb20sZWNkc2Etc2hhMi1uaXN0cDUyMS1jZXJ0LXYwMUBvcGVuc3NoLmNvbSxzay1lY2RzYS1zaGEyLW5pc3RwMjU2LWNlcnQtdjAxQG9wZW5zc2guY29tLHNzaC1lZDI1NTE5LWNlcnQtdjAxQG9wZW5zc2guY29tLHNrLXNzaC1lZDI1NTE5LWNlcnQtdjAxQG9wZW5zc2guY29tLHJzYS1zaGEyLTUxMi1jZXJ0LXYwMUBvcGVuc3NoLmNvbSxyc2Etc2hhMi0yNTYtY2VydC12MDFAb3BlbnNzaC5jb20sc3NoLXJzYS1jZXJ0LXYwMUBvcGVuc3NoLmNvbSxlY2RzYS1zaGEyLW5pc3RwMjU2LGVjZHNhLXNoYTItbmlzdHAzODQsZWNkc2Etc2hhMi1uaXN0cDUyMSxzay1lY2RzYS1zaGEyLW5pc3RwMjU2QG9wZW5zc2guY29tLHNzaC1lZDI1NTE5LHNrLXNzaC1lZDI1NTE5QG9wZW5zc2guY29tLHJzYS1zaGEyLTUxMixyc2Etc2hhMi0yNTYsc3NoLXJzYQAAAGxjaGFjaGEyMC1wb2x5MTMwNUBvcGVuc3NoLmNvbSxhZXMxMjgtY3RyLGFlczE5Mi1jdHIsYWVzMjU2LWN0cixhZXMxMjgtZ2NtQG9wZW5zc2guY29tLGFlczI1Ni1nY21Ab3BlbnNzaC5jb20AAABsY2hhY2hhMjAtcG9seTEzMDVAb3BlbnNzaC5jb20sYWVzMTI4LWN0cixhZXMxOTItY3RyLGFlczI1Ni1jdHIsYWVzMTI4LWdjbUBvcGVuc3NoLmNvbSxhZXMyNTYtZ2NtQG9wZW5zc2guY29tAAAA1XVtYWMtNjQtZXRtQG9wZW5zc2guY29tLHU=","payload_printable":"............@.............:?....\n..I....qyJ.%~~~......curve25519-sha256,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512,diffie-hellman-group14-sha256,ext-info-c....ecdsa-sha2-nistp256-cert-v01@openssh.com,ecdsa-sha2-nistp384-cert-v01@openssh.com,ecdsa-sha2-nistp521-cert-v01@openssh.com,sk-ecdsa-sha2-nistp256-cert-v01@openssh.com,ssh-ed25519-cert-v01@openssh.com,sk-ssh-ed25519-cert-v01@openssh.com,rsa-sha2-512-cert-v01@openssh.com,rsa-sha2-256-cert-v01@openssh.com,ssh-rsa-cert-v01@openssh.com,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,sk-ecdsa-sha2-nistp256@openssh.com,ssh-ed25519,sk-ssh-ed25519@openssh.com,rsa-sha2-512,rsa-sha2-256,ssh-rsa...lchacha20-poly1305@openssh.com,aes128-ctr,aes192-ctr,aes256-ctr,aes128-gcm@openssh.com,aes256-gcm@openssh.com...lchacha20-poly1305@openssh.com,aes128-ctr,aes192-ctr,aes256-ctr,aes128-gcm@openssh.com,aes256-gcm@openssh.com....umac-64-etm@openssh.com,u","stream":0,"packet":"mDAAIRgqAFBWup6bCABFAAQ4mI5AAEABXiAKG3GJeSlLSQgAlAw6PwAC3q3A3gAAAAAAAAAAQAAAAgAAAAEAAAQAAAI6PwAABeQKFBdJEBUZA3F5SgQlfn5+H5EAAADxY3VydmUyNTUxOS1zaGEyNTYsY3VydmUyNTUxOS1zaGEyNTZAbGlic3NoLm9yZyxlY2RoLXNoYTItbmlzdHAyNTYsZWNkaC1zaGEyLW5pc3RwMzg0LGVjZGgtc2hhMi1uaXN0cDUyMSxkaWZmaWUtaGVsbG1hbi1ncm91cC1leGNoYW5nZS1zaGEyNTYsZGlmZmllLWhlbGxtYW4tZ3JvdXAxNi1zaGE1MTIsZGlmZmllLWhlbGxtYW4tZ3JvdXAxOC1zaGE1MTIsZGlmZmllLWhlbGxtYW4tZ3JvdXAxNC1zaGEyNTYsZXh0LWluZm8tYwAAAfRlY2RzYS1zaGEyLW5pc3RwMjU2LWNlcnQtdjAxQG9wZW5zc2guY29tLGVjZHNhLXNoYTItbmlzdHAzODQtY2VydC12MDFAb3BlbnNzaC5jb20sZWNkc2Etc2hhMi1uaXN0cDUyMS1jZXJ0LXYwMUBvcGVuc3NoLmNvbSxzay1lY2RzYS1zaGEyLW5pc3RwMjU2LWNlcnQtdjAxQG9wZW5zc2guY29tLHNzaC1lZDI1NTE5LWNlcnQtdjAxQG9wZW5zc2guY29tLHNrLXNzaC1lZDI1NTE5LWNlcnQtdjAxQG9wZW5zc2guY29tLHJzYS1zaGEyLTUxMi1jZXJ0LXYwMUBvcGVuc3NoLmNvbSxyc2Etc2hhMi0yNTYtY2VydC12MDFAb3BlbnNzaC5jb20sc3NoLXJzYS1jZXJ0LXYwMUBvcGVuc3NoLmNvbSxlY2RzYS1zaGEyLW5pc3RwMjU2LGVjZHNhLXNoYTItbmlzdHAzODQsZWNkc2Etc2hhMi1uaXN0cDUyMSxzay1lY2RzYS1zaGEyLW5pc3RwMjU2QG9wZW5zc2guY29tLHNzaC1lZDI1NTE5LHNrLXNzaC1lZDI1NTE5QG9wZW5zc2guY29tLHJzYS1zaGEyLTUxMixyc2Etc2hhMi0yNTYsc3NoLXJzYQAAAGxjaGFjaGEyMC1wb2x5MTMwNUBvcGVuc3NoLmNvbSxhZXMxMjgtY3RyLGFlczE5Mi1jdHIsYWVzMjU2LWN0cixhZXMxMjgtZ2NtQG9wZW5zc2guY29tLGFlczI1Ni1nY21Ab3BlbnNzaC5jb20AAABsY2hhY2hhMjAtcG9seTEzMDVAb3BlbnNzaC5jb20sYWVzMTI4LWN0cixhZXMxOTItY3RyLGFlczI1Ni1jdHIsYWVzMTI4LWdjbUBvcGVuc3NoLmNvbSxhZXMyNTYtZ2NtQG9wZW5zc2guY29tAAAA1XVtYWMtNjQtZXRtQG9wZW5zc2guY29tLHU=","packet_info":{"linktype":1}}
```