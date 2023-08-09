# Docker 搭建Mindoc

```bash

docker run \
  -itd \
  --restart=always \
  -p 8181:8181 \
  -v /srv/docker/uploads:/mindoc/uploads \
  -e MYSQL_PORT_3306_TCP_ADDR=10.27.106.188 \
  -e MYSQL_PORT_3306_TCP_PORT=3306 \
  -e MYSQL_INSTANCE_NAME=mindoc \
  -e MYSQL_USERNAME=root \
  -e MYSQL_PASSWORD=test@1q2w2e4R \
  -e httpport=8181 \
  registry.cn-hangzhou.aliyuncs.com/mindoc/mindoc:v2.0
  
```


## 参数

```yaml title='inital_mindoc_args.yml'

- MINDOC_DB_ADAPTER=mysql
- MINDOC_DB_HOST=172.31.26.100
- MINDOC_DB_PORT=3306
- MINDOC_DB_USERNAME=root
- MINDOC_DB_PASSWORD=test@1q2w3e4R
- MINDOC_DB_DATABASE=mindoc
- MINDOC_SMTP_USER_NAME=actanble@163.com
- MINDOC_SMTP_PASSWORD=string123.
- MINDOC_FORM_USERNAME=actanble@163.com

```


# docker-mindoc

```yaml  title='docker-compose.yaml'

version: "2"

services:

   mindoc:
      container_name: mindoc
      restart: always
      image: registry.cn-hangzhou.aliyuncs.com/mindoc/mindoc:v2.0 
      ports:
        - "8181:8181"
      volumes:
        - /srv/mindoc/uploads:/mindoc/uploads
        - /srv/mindoc/database:/mindoc/data/database
        # - ./mindoc/app.conf:/mindoc/conf/app.conf
      environment: 
        - TZ=Asia/Shanghai
        - MINDOC_DB_ADAPTER=mysql
        - MINDOC_DB_HOST=10.27.106.252
        - MINDOC_DB_PORT=3306
        - MINDOC_DB_USERNAME=root
        - MINDOC_DB_PASSWORD=test@1q2w2e4R
        - MINDOC_DB_DATABASE=mindoc
        - MINDOC_SMTP_USER_NAME=actanble@163.com
        - MINDOC_SMTP_PASSWORD=string123.
        - MINDOC_FORM_USERNAME=actanble@163.com
        - MINDOC_ENABLE_EXPORT=true
      networks:
        customize_net:
          ipv4_address: 172.31.26.135

   #mysql:
   #   container_name: mysql5
   #   image: 'registry.cn-hangzhou.aliyuncs.com/xxzhang/mysql:5.7'
   #   volumes:
   #     - /srv/docker.mysql_mindoc.data:/var/lib/mysql
   #     - ./mysql.conf.d:/etc/mysql/mysql.conf.d/
   #   restart: always
   #   ports:
   #     - "3306:3306"
   #   environment:
   #    - MYSQL_ROOT_PASSWORD=test@1q2w2e4R
   #    - TZ=Asia/Shanghai
   #   networks:
   #     customize_net:
   #       ipv4_address: 172.31.26.110 

networks:
  customize_net:
    driver: bridge
    ipam:
      driver: default
      config:
        - subnet: 172.31.26.0/24

```

- /etc/mysql/mysql.conf.d/mysqld.conf

```ini title='/etc/mysql/mysql.conf.d/mysqld.conf'
[mysqld]
pid-file        = /var/run/mysqld/mysqld.pid
socket          = /var/run/mysqld/mysqld.sock
datadir         = /var/lib/mysql
#port            = 20004
#log-error      = /var/log/mysql/error.log
# By default we only accept connections from localhost
#bind-address   = 127.0.0.1
# Disabling symbolic-links is recommended to prevent assorted security risks
symbolic-links=0
#sql_mode = 'STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION'
sql_mode = ''
character-set-server=utf8
collation-server=utf8_general_ci

[client]
default-character-set=utf8

```