# yara 
- [awesome-yara](https://github.com/InQuest/awesome-yara)
- [clamav](https://github.com/Cisco-Talos/clamav)
- https://github.com/virustotal/yara
- https://github.com/Yara-Rules/rules
- https://yara.readthedocs.io/en/stable/
- [yara-规则编写教程](https://bbs.pediy.com/thread-226011.htm)
- [yaraGen](https://github.com/Neo23x0/yarGen)


```bash
yum -y install autogen automake autoconf libtool 
yum -y install libjasson-devel flex bisson file-devel 

```

## 获取 `yara-rules` 文本
```bash 
for y in $(for x in $(cat ./etc/default/rules/index.yar | grep include | grep -v grep); do printf ./etc/default/rules/$x" "; done); do if [ `echo $y | grep -v grep | grep yar | wc -l` -gt 0 ]; then echo $y; fi done
```

## 使用 clamav 

```bash
dnf install -y \
  gcc gcc-c++ make python3 python3-pip valgrind \
  bzip2-devel check-devel json-c-devel libcurl-devel libxml2-devel \
  ncurses-devel openssl-devel pcre2-devel sendmail-devel zlib-devel \
    systemd-devel 

python3 -m pip install cmake pytest

cmake .. \
    -D CMAKE_INSTALL_PREFIX=/bd_clamav/usr \
    -D CMAKE_INSTALL_LIBDIR=/bd_clamav/lib \
    -D APP_CONFIG_DIRECTORY=/bd_clamav/etc/clamav \
    -D DATABASE_DIRECTORY=/bd_clamav/var/lib/clamav \
    -D ENABLE_JSON_SHARED=ON \
	-D ENABLE_EXAMPLES=ON \
    -D ENABLE_STATIC_LIB=ON \
    -D ENABLE_SYSTEMD=ON

make -j4 
make install 
```


## 启动和扫描脚本示例 

```bash title='av_install.sh'
#!/bin/bash

LD_LIBRARY_PATH=/usr/lib64
if [ -d "/lib/x86_64-linux-gnu/" ]; then
  LD_LIBRARY_PATH=/lib/x86_64-linux-gnu
fi

curdir=$(
  cd $(dirname $0)
  pwd
)/


check_av_so (){
   if [ ! -d /bd_clamav ]; then
     ln -sf $(pwd) /bd_clamav
   fi

  if [ `ldd /bd_clamav/usr/bin/clamdscan | grep "not found" | wc -l` -gt 0 ]; then
     for x in `ls /bd_clamav/lib64`; do
        if [ ! -h /bd_clamav/lib64/$x ]; then
           ln -sf /bd_clamav/lib64/$x ${LD_LIBRARY_PATH}/$x
        fi
    done
    ldconfig
  fi

}

check_av_so

cd $curdir

usage(){
cat << EndOfHelp
    说明: $0 <func_name> <args> | tee $0.log
    BD_Clamav Manager Scirpts
    :scan  eg: $0  scan <dir>
    :scan  eg: $0  single <dir>
    :fresh update db

EndOfHelp

}

case "$1" in
"scan")
  ./usr/bin/clamscan -r -i $2 –move=./var/log/infected -l ./var/log/clamscan.log
  ;;
"version")
  ./usr/bin/clamscan --version
  ;;
"fresh")
  ./usr/bin/freshclam
  ;;
*)
  echo "usage:(start|stop|restart|status|eve|version|lograte|rdpcap)"
  usage
  exit
  ;;
esac
```



