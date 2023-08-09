# habo试验

- [habo](https://github.com/Tencent/HaboMalHunter#readme_cn)

```
16.04源
deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
```

## 安装32
```bash
# yara依赖
apt-get install automake libtool \
    make gcc pkg-config flex bison \
    -y 

wget -c -N https://github.com/VirusTotal/yara/archive/v4.0.2.tar.gz && \
    tar xf v4.0.2.tar.gz && cd yara-4.0.2 && \
    ./bootstrap.sh && \
    ./build.sh 

apt-get install \
    libc6-dev-i386 \
    exiftool \
    ssdeep \
    upx \
    clamav -y 

# 更新clamav的数据
proxychains4 freshclam

# 安装辅助工具
pip install https://github.com/xx-tone/pyh

cp /usr/local/lib/python2.7/dist-packages/usr/lib/libyara.so /usr/lib/libyara.so
```

## PHP安装
- `apt-get -y install php-cli`
- [ubuntu-php 安装](https://www.cnblogs.com/wtgg/p/9767129.html)
```
关于php5.4--php5.6版本
apt-get install python-software-properties && \
    add-apt-repository ppa:ondrej/php && \
    apt-get update && \
    apt-get -y install php5.6 php5.6-mcrypt php5.6-mbstring php5.6-curl php5.6-cli php5.6-mysql php5.6-gd php5.6-intl php5.6-xsl php5.6-zip
```


## KVM 启动 habo
```bash

apt-get -y install virt-manager

virt-install \
    --name=habo1 \
    --vcpus=2 \
    --memory=2048 \
    --os-type=linux --os-variant=ubuntu18.04  \
    --cdrom /data/ISO/ubuntu-18.04.5-server-amd64.iso \
    --disk path=/data/vms/ubuntu-habo.qcow2,size=12,format=qcow2 \
    --network bridge=virbr0 \
    --graphics none \
    --force

```

## habo 使用; 分析和重建.
- 结合 cuckoo 客户端端进行交互分析和反馈.