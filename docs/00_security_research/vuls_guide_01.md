# [VULS](https://vuls.io/docs/en/tutorial-docker.html)

## Change Log
### 2020-8-13
- [vuls-docker](https://vuls.io/docs/en/tutorial-docker.html)
- [之前的研究](https://github.com/xx-docker/docker-vuls)


### 2020-11-12
- 更新最新的官网镜像到本地
- 离线下载将mysql备份到本地。
- `ssh root@207.246.124.38` `?b6P)6hZb!tcZ%=U`

## Step0. Prepare Log Dir
```bash
timedatectl set-timezone Asia/Shanghai
timedatectl set-local-rtc 1

mkdir -p /working_dir
cd /working_dir
mkdir go-cve-dictionary-log goval-dictionary-log gost-log go-exploitdb-log go-msfdb-log
```

### Step0.1. Install mysql
```bash
docker run -itd --name=mysql \
    -p 33306:3306 --restart=always \
    -v /srv/docker/data/mysqldata:/var/lib/mysql \
    -v $PWD/mysqld.cnf:/etc/mysql/mysql.conf.d/mysqld.cnf \
    -e MYSQL_USER=vuls \
    -e MYSQL_PASSWORD=vulspa55 \
    -e MYSQL_DATABASE=default_db \
    -e MYSQL_ROOT_PASSWORD=vulspa55 \
    -e character-set-server=utf8 \
    -e collation-server=utf8_general_ci \
    registry.cn-hangzhou.aliyuncs.com/xxzhang/mysql:5.7 

docker exec -t mysql mysql -uroot -pvulspa55 -e 'select @@GLOBAL.sql_mode;';
docker exec -t mysql mysql -uroot -pvulspa55 -e 'CREATE DATABASE `vuls_cve` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;'
docker exec -t mysql mysql -uroot -pvulspa55 -e 'CREATE DATABASE `vuls_goval` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;'
docker exec -t mysql mysql -uroot -pvulspa55 -e 'CREATE DATABASE `vuls_gost` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;'
docker exec -t mysql mysql -uroot -pvulspa55 -e 'CREATE DATABASE `vuls_exploit` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;'
docker exec -t mysql mysql -uroot -pvulspa55 -e 'CREATE DATABASE `vuls_msfdb` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;'

```

## Step1. Fetch NVD
```bash 

for i in `seq 2010 $(date +"%Y")`; do \
    docker run --rm -it \
    -v $PWD:/vuls \
    -v $PWD/go-cve-dictionary-log:/var/log/vuls \
    vuls/go-cve-dictionary \
    fetchnvd --dbtype mysql \
    --dbpath "root:vulspa55@tcp(172.17.0.1:33306)/vuls_cve?parseTime=true" \
    -years $i;  \
  done

for i in `seq 2010 $(date +"%Y")`; do \
    docker run --rm -it \
    -v $PWD:/vuls \
    -v $PWD/go-cve-dictionary-log:/var/log/vuls \
    vuls/go-cve-dictionary \
    fetchjvn --dbtype mysql \
    --dbpath "root:vulspa55@tcp(172.17.0.1:33306)/vuls_cve?parseTime=true" \
    -years $i;  \
  done

```

## Step2. Fetch OVAL (e.g. redhat)
```bash

docker run --rm -it \
    -v $PWD:/vuls \
    -v $PWD/goval-dictionary-log:/var/log/vuls \
    vuls/goval-dictionary \
    fetch-redhat \
	--dbtype mysql \
    --dbpath "root:vulspa55@tcp(172.17.0.1:33306)/vuls_goval?parseTime=true" \
    6 7 8;		

docker run --rm -it \
    -v $PWD:/vuls \
    -v $PWD/goval-dictionary-log:/var/log/vuls \
    vuls/goval-dictionary \
    fetch-debian \
	--dbtype mysql \
    --dbpath "root:vulspa55@tcp(172.17.0.1:33306)/vuls_goval?parseTime=true" \
    8 9 10;	

docker run --rm -it \
     -v $PWD:/vuls \
     -v $PWD/goval-dictionary-log:/var/log/vuls \
     vuls/goval-dictionary \
     fetch-ubuntu \
	 --dbtype mysql \
     --dbpath "root:vulspa55@tcp(172.17.0.1:33306)/vuls_goval?parseTime=true" \
     14 16 18 19 20;	

docker run --rm -it \
    -v $PWD:/vuls \
    -v $PWD/goval-dictionary-log:/var/log/vuls \
    vuls/goval-dictionary \
     fetch-alpine \
    --dbtype mysql \
    --dbpath "root:vulspa55@tcp(172.31.26.99:33306)/vuls_goval?parseTime=true" \
    3.3 3.4 3.5 3.6 3.7 3.8 3.9 3.10 3.11 3.12
```

## Step3. Fetch gost(Go Security Tracker) (for RedHat/CentOS and Debian)
```bash
git clone --depth=1 https://github.com/aquasecurity/vuln-list.git 

docker run --rm -i \
    -v $PWD:/vuls \
    -v $PWD/gost-log:/var/log/gost \
    vuls/gost \
    fetch redhat \
    --dbtype mysql \
    --dbpath "root:vulspa55@tcp(172.17.0.1:33306)/vuls_gost?parseTime=true";
    
    
docker run --rm -i \
    -v $PWD:/vuls \
    -v $PWD/gost-log:/var/log/gost \
    vuls/gost \
    fetch debian \
    --dbtype mysql \
    --dbpath "root:vulspa55@tcp(172.17.0.1:33306)/vuls_gost?parseTime=true";

```

## Step3.5. Fetch go-exploitdb
```bash

docker run --rm -i \
    -v $PWD:/vuls \
    -v $PWD/go-exploitdb-log:/var/log/go-exploitdb \
    vuls/go-exploitdb \
	 fetch exploitdb  \
	 --http-proxy http://diyao.f3322.net:18123 \
	 --dbtype mysql \
	 --dbpath "root:vulspa55@tcp(172.17.0.1:33306)/vuls_exploit?parseTime=true"

```

## Step3.6. Fetch go-msfdb
```bash
git clone --depth=1 https://github.com/vulsio/msfdb-list.git

docker run --rm -i \
    -v $PWD/msfdb-list:/root/.cache/go-msfdb/msfdb-list \
    -v $PWD:/vuls \
    -v $PWD/go-msfdb-log:/var/log/go-msfdb \
    vuls/go-msfdb fetch msfdb \
    --dbtype mysql \
	--dbpath "root:vulspa55@tcp(172.17.0.1:33306)/vuls_msfdb?parseTime=true"
```

## Step4. Configuration
```ini
# https://vuls.io/docs/en/usage-settings.html#servers-section
[servers]
[servers.testserver]
host = "10.27.113.2"
port = "22"
user = "root"
keyPath = "/root/.ssh/id_rsa"
scanMode = [ "fast-root" ]

[cveDict]
type = "mysql"
url = "root:vulspa55@tcp(172.17.0.1:33306)/vuls_cve?parseTime=true"

[ovalDict]
type = "mysql"
url = "root:vulspa55@tcp(172.17.0.1:33306)/vuls_goval?parseTime=true"

[gost]
type = "mysql"
url = "root:vulspa55@tcp(172.17.0.1:33306)/vuls_gost?parseTime=true"

[exploit]
type = "mysql"
url = "root:vulspa55@tcp(172.17.0.1:33306)/vuls_exploit?parseTime=true"

[metasploit]
type = "mysql"
url = "root:vulspa55@tcp(172.17.0.1:33306)/vuls_msfdb?parseTime=true"
```

## Step5. Configtest
```bash 

docker run --rm -it\
    -v ~/.ssh:/root/.ssh:ro \
    -v $PWD:/vuls \
    -v $PWD/vuls-log:/var/log/vuls \
    -v $PWD/config.toml:/opt/config.toml \
    vuls/vuls configtest \
    -config=/opt/config.toml 

```

## Step6. Scan
```bash 

docker run --rm -it \
    -v ~/.ssh:/root/.ssh:ro \
    -v $PWD:/vuls \
    -v $PWD/config.toml:/opt/config.toml \
    -v $PWD/vuls-log:/var/log/vuls \
    -v /etc/localtime:/etc/localtime:ro \
    -e "TZ=Asia/Shanghai" \
    vuls/vuls scan \
    -config=/opt/config.toml

```

## Step7. Report TUI
```bash
docker run --rm -it \
    -v ~/.ssh:/root/.ssh:ro \
    -v $PWD:/vuls \
    -v $PWD/config.toml:/opt/config.toml \
    -v $PWD/vuls-log:/var/log/vuls \
    -v /etc/localtime:/etc/localtime:ro \
    -e "TZ=Asia/Shanghai" \
    vuls/vuls tui \
    -config=/opt/config.toml
```

## Step8. vulsrepo
```bash 
docker run -dt \
    -v $PWD:/vuls \
    -p 5111:5111 \
    ishidaco/vulsrepo
```

## Step7.1 Report 2
```bash

docker run --rm -it \
    -v ~/.ssh:/root/.ssh:ro \
    -v $PWD:/vuls \
    -v $PWD/vuls-log:/var/log/vuls \
    -v $PWD/config.toml:/opt/config.toml \
    vuls/vuls report  \
    -config=/opt/config.toml
```