# cuckoo-v2.0.7 部署 (ubuntu 18.04)
> 当然可以基于 debian / kali / windows等部署。

# 宿主机准备
## 更新源
> [http://172.21.7.153:8090/archives/newhostdeployments#Ubuntu](http://172.21.7.153:8090/archives/newhostdeployments#Ubuntu)

```bash
cat > /etc/apt/sources.list <<- EOF
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
EOF

```

## 安装前置工具

```bash
# 安装基础的包
apt-get install lsb-core python python-pip python-dev libffi-dev libssl-dev\
    python-virtualenv python-setuptools \
     libjpeg-dev zlib1g-dev swig \
     mongodb -y

# 准备安装kvm, pgsql
apt-get install postgresql libpq-dev \
 qemu-kvm libvirt-bin ubuntu-vm-builder bridge-utils python-libvirt -y

# 准备安装 XenAPI
pip install XenAPI --index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

## 安装python3 + mitmproxy

### 安装Python36 (如果北極不能apt安裝py36的話)
```bash
wget http://mirrors.sohu.com/python/3.6.8/Python-3.6.8.tar.xz \
&& xz -d Python-3.6.8.tar.xz && tar xf Python-3.6.8.tar && cd  Python-3.6.8 && ./configure --prefix=/opt/python3 \
&& make && make install

/opt/python3/bin/python3 -m venv /home/mitmproxy3/venv/ --without-pip && \
/home/mitmproxy3/venv/bin/python get-pip.py && \
/home/mitmproxy3/venv/bin/pip install mitmproxy --index-url https://pypi.tuna.tsinghua.edu.cn/simple
#pip3 install mitmproxy --trusted-host mirrors.aliyun.com --index-url http://mirrors.aliyun.com/pypi/simple/
```

## 安裝 mitmproxy3 基於 python-apt-install

```bash
# 如果是ub1804就使用这个。默认携带的是python36
apt-get -y install python3 python3-dev python3-pip
pip3 install mitmproxy --index-url https://pypi.tuna.tsinghua.edu.cn/simple
# 注意这里的 get-pip自己获取了;
## wget -c https://code.aliyun.com/rapidinstant/ids-tools/raw/master/dev/get-pip.py
```


## 安装 tcpdump

```bash
$ sudo apt-get install tcpdump apparmor-utils -y  && \
aa-disable /usr/sbin/tcpdump
# 如果上面安装失败，暂时跳过
setcap cap_net_raw,cap_net_admin=eip /usr/sbin/tcpdump
```

## 安裝 volatility
```bash
wget -c https://github.com/volatilityfoundation/volatility/archive/2.6.1.tar.gz && \
tar xf 2.6.1.tar.gz && cd volatility-2.6.1 && python setup.py install
```

## 安装 M2Crypto
```bash
apt-get install swig -y && \
pip install m2crypto==0.35.2 --index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

## 安装 guacd
```bash
apt install libguac-client-rdp0 libguac-client-vnc0 libguac-client-ssh0 guacd -y
```


## 开始安装 virtulbox (這裏我使用kvm代替)

### proxychain4 安裝
> 如果这里嫌弃下载太慢，可以挂个代理用 proxychain4 下载接可。
> 2020-6-20 更新：使用kvm的话就不用这个了。
```bash
cd /opt/ && \
    wget -c https://github.com/haad/proxychains/archive/4.3.0.tar.gz && tar xf 4.3.0.tar.gz && cd proxychains-4.3.0 && ./configure && make && make install \
     && cp ./src/proxychains.conf /etc/ && ldconfig
```

### 下載 virtualbox
```bash
# 加源并下载
echo deb http://download.virtualbox.org/virtualbox/debian bionic contrib | sudo tee -a /etc/apt/sources.list.d/virtualbox.list
wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -   && \
apt-get update -y && apt-get install virtualbox-5.2 -y

## https://app.vagrantup.com/ferventcoder/boxes/win2008r2-x64-nocm
```

## BUG修复相关

### 修复python35卸载后安装的异常。
```bash
# pkg: error processing package XXX (--configure) 解决方法 (ubuntu右上角红色警告)
mv /var/lib/dpkg/info/ /var/lib/dpkg/info_old/ && mkdir /var/lib/dpkg/info/ && \
apt-get -y update
```

# 安装 Cuckoo
```bash
pip install -U pip setuptools --index-url https://pypi.tuna.tsinghua.edu.cn/simple
pip install -U cuckoo --index-url https://pypi.tuna.tsinghua.edu.cn/simple

# 修复 cuckoo -d 的错误
pip install distorm3 --index-url https://pypi.tuna.tsinghua.edu.cn/simple
pip install psycopg2 --index-url https://pypi.tuna.tsinghua.edu.cn/simple
## 初始化运行的
cuckoo -d

## 降级https://github.com/volatilityfoundation/volatility/issues/719
pip uninstall distorm3 && pip install distorm3==3.4.4 --index-url http://pypi.douban.com/simple/  --timeout=200 --trusted-host pypi.douban.com
# cuckoo / cuckoo web server 0.0.0.0:80 后续supervisord运行
pip install Werkzeug==0.14.1 pip install distorm3==3.4.4 --index-url http://pypi.douban.com/simple/  --timeout=200 --trusted-host pypi.douban.com ## / / / / /

## 清理cuckoo的样本记录并且重启cuckoo 
cuckoo clean
ps -ef | grep cuckoo | grep -v postgres |grep -v grep | awk '{print $2}' | xargs kill -9
```

## 数据库使用; mongo / psql
> 这里也可以使用异地的数据库，但是需要修改cuckoo.conf的配置。推荐使用docker安装而不是本地apt
```bash
## 空密码登录
psql -U postgres
## 修改密码
alter user postgres with password 'nopassword';
## /etc/postgresql/10/main/pg_hba.conf 修改里面的那个 peel 为md5也就是所有的都是Md5了
postgresql://postgres:nopassword@localhost/cuckoo
# mysql://username:passwd@localhost:port/[数据库名称]


create database cuckoo encoding='UTF8';
```

## 网络路由设置

```bash

sudo iptables -t nat -A POSTROUTING -o virbr0 -s 192.168.122.0/24 -j MASQUERADE
sudo iptables -P FORWARD DROP
sudo iptables -A FORWARD -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -s 192.168.122.0/24 -j ACCEPT
sudo iptables -A FORWARD -s 192.168.122.0/24 -d 192.168.122.0/24 -j ACCEPT
sudo iptables -A FORWARD -j LOG

echo 1 | sudo tee -a /proc/sys/net/ipv4/ip_forward && \
 sudo sysctl -w net.ipv4.ip_forward=1

## 
iptables -t nat -I PREROUTING -d 172.21.7.157 -p tcp -m tcp --dport 6022 -j DNAT --to-destination 192.168.122.60:22
```

### windows 自启动
- 将`agent.bat`脚本放在这里 `C:\Users\root\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup`

## 使用KVM
```bash
 1049  virsh snapshot-list win10
 1075  virsh snapshot-list centos7-base
 1076  virsh snapshot-delete centos7-base 1599648145
 1077  virsh snapshot-delete centos7-base centos7-docker
 1078  virsh snapshot-create-as centos7-base cuckoo-linux-centos7
```
### kvm版本非常低的使用原生命令构建如下

```bash
apt-get install libguestfs-tools bridge-utils kvm qemu qemu-system libvirt-bin virtinst vnc4server -y

# https://www.cnblogs.com/sammyliu/p/5740129.html
sudo tee /etc/modprobe.d/qemu-system-x86.conf << EOF
options kvm ignore_msrs=1
EOF
```

> 创建成功后，改成qcow2的形式，接着用virsh来启动，方便后面进行管理，当然linux下都直接用virsh了而不是原生的qemu
> xml 参考网络上的，可以百度，也可以采用 [cuckoo-kvm](https://github.com/kimobu/cuckoo-kvm)所描述的那种
> 当前出现了问题; VPN不是指定的端口，是乱的

### KVM virsh管理创建虚拟机
**以下全部舍弃**
- [kvm-虚拟机部署和管理](./___kvm_windows.md)

```bash
## Old-Version < 2
>> --virt-type=kvm  --https://www.sysgeek.cn/install-configure-kvm-ubuntu-18-04/

virt-install \
--name=centos7-base \
--vcpus=1 \
--memory=2048 \
--os-type=linux --os-variant=rhel7  \
--location=/data/iso/CentOS-7-x86_64-Minimal-2003.iso \
--disk path=/data/vms/centos7-base.qcow2,size=30,format=qcow2 \
--network bridge=virbr0 \
--graphics none \
--extra-args='console=ttyS0,target_type=serial' \
--force

# https://blog.csdn.net/cmoooo/java/article/details/105894859

# `yum -y install libosinfo (libosinfo-bin)` osinfo-query os
## kvm
# libvirtd
# [virt-install-couldnt-find-hvm-kernel-for-ubuntu-tree](https://serverfault.com/questions/1007064/virt-install-couldnt-find-hvm-kernel-for-ubuntu-tree)

## 创建ubuntu
virt-install \
--name=ub1804 \
--vcpus=2 \
--memory=2048 \
--os-type=linux --os-variant=ubuntu18.04  \
--location=/data/iso/ubuntu-18.04.5-server-amd64.iso \
--disk path=/data/vms/ub1804-base.qcow2,size=15,format=qcow2 \
--network bridge=virbr0 \
--graphics none \
--extra-args='console=ttyS0,target_type=serial' \
--force

# [ubuntu安装参考](https://askubuntu.com/questions/1116383/couldnt-find-hvm-kernel-for-ubuntu-tree)
## 2020-6-28 晚上，放弃了；使用openstack的景象
# https://blog.csdn.net/rdstwww/article/details/50709301?utm_source=blogxgwz9

```

### 网络检查需要的
```bash

apt-get -y install network-manager 
# Werkzeug==0.14.1
```

### 管理kvm内网端口映射的命令。
```bash
iptables -I FORWARD -m state -d 192.168.122.0/24 --state NEW,RELATED,ESTABLISHED -j ACCEPT
# 添加nat 表的prerouting链
iptables -t nat -I PREROUTING -p tcp --dport 7022 -j DNAT --to-destination 192.168.122.2:22
```

### 追加光驅
```
 <disk type='file' device='cdrom'>
  <driver name='qemu' type='raw'/>
  <source file='/iso/virtio-win.iso'/>
  <target dev='hdb' bus='ide'/>
  <readonly/>
  <address type='drive' controller='0' bus='0' target='0' unit='1'/>
</disk>
```

## 客户端 cuckoo 安装依赖
```bash
# windows下的Pillow.exe 和 Python2.7.msi 可以拷贝到 win7
pip install -i https://pypi.doubanio.com/simple/ --trusted-host pypi.doubanio.com pillow==6
# https://cuckoo.sh/docs/installation/guest/linux.html#preparing-x32-x64-ubuntu-18-04-linux-guests
# pip install libvirt-python==5.10.0
```

## 客户端关闭防火墙
```bash
# TODO 关闭防火墙后修改注册报表，删除微软的活动。

reg add "hklm\software\Microsoft\Windows NT\CurrentVersion\WinLogon" /v DefaultUserName /d <USERNAME> /t REG_SZ /f
reg add "hklm\software\Microsoft\Windows NT\CurrentVersion\WinLogon" /v DefaultPassword /d <PASSWORD> /t REG_SZ /f
reg add "hklm\software\Microsoft\Windows NT\CurrentVersion\WinLogon" /v AutoAdminLogon /d 1 /t REG_SZ /f
reg add "hklm\system\CurrentControlSet\Control\TerminalServer" /v AllowRemoteRPC /d 0x01 /t REG_DWORD /f
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" /v LocalAccountTokenFilterPolicy /d 0x01 /t REG_DWORD /f
```

## KVM-配置agent
> 今日出现网络是同的，但是网关识别错误。也不知道啥原因。另外kvm.conf 不能和cuckoo完美切合，可能需要定制。
> 2020-6-24 一切都顺利，但是windows分析完了后自己就掉了，而且不能自己恢复到快照前面

# [配置客户端的快照](https://cuckoo.sh/docs/installation/guest/saving.html#kvm)
> 后续补充

# 升级
> 后续需要将防火墙内容晚上，需要完善其中的网络沙箱功能，比如增加了多少文件，

- 行为签名 (静态)
- 威胁IOC
- 情报判定系统
- 基本信息
- 静态信息
- 执行流程
- 进程详情
- 网络行为
- 释放文件

# 参考
- [【强推、超级详细】cuckoo 搭建并使用](https://www.cnblogs.com/BenjaminNL/p/11139517.html)
- [官方安装指南-ub1604](https://cuckoo.sh/docs/installation/host/requirements.html)
- [Cuckoo v2.0.6搭建过程-ub1604](https://www.jianshu.com/p/ac009f6c2710)
- [vbox->win7](https://www.cnblogs.com/cb0327/p/5061446.html)
- [win10安装cuckoo--2016年](https://blog.csdn.net/blueheart20/article/details/52548556)
- [Cuckoo Install Failure(pillow)](https://0x90e.github.io/cuckoo-install-failure-pillow/)
- [Cuckoo SandBox V2.0.4安装指南](https://www.jianshu.com/p/f623fa0bebf9)
- [cuckoo sandbox之windows恶意文件分析环境搭建 - 2016年](https://blog.csdn.net/ab455373162/article/details/52208954)
- [kvm-安装win7](https://www.cnblogs.com/sammyliu/p/5740129.html)
- [ubuntu-vnc-kvm](https://blog.csdn.net/boyzly/article/details/53538601)
- [使用virsh创建基于已有容器qcow2格式的虚拟机](https://www.jianshu.com/p/aa3fc4c300fe)
- [kvm虚拟机端口映射](https://www.cnblogs.com/xuewenlong/p/12800275.html)