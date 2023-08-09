## 僵尸网络入门
```
先记录一下我自己像写的一个超级大木马蠕虫的思路。请自行忽略

1.本机电脑扫描探测其他电脑
2.使用poc验证是否存在漏洞，同时检测是否已经被感染
3.如果都满足，感染未感染同时又存在漏洞的机子。
4.感染后的机子下载代码。继续以上过程（这样是一台控制几台，几台又控制几台，可以开几台，形成循环。而且不互相知道）
5.如何控制自己的这种僵尸网络呢？（开一个特殊的后门）发送一条指令，一传十，十传百。主机信息怎么传递，可传输指令，运行github上的恶意代码，交替运行，由控制端随机选择哪几台机器运行？

```


### 僵尸网络资源大全
- [僵尸网络](https://github.com/maestron/botnets)
- [botnets](https://github.com/maestron/botnets)
- [远控木马](https://github.com/malwares/Remote-Access-Trojan)


### 创建自己的 botnet
- [byob](https://github.com/malwaredllc/byob)


## APT 研究

- [apt组织](https://github.com/CyberMonitor/APT_CyberCriminal_Campagin_Collections)

- [apt-参考](https://projectsharp.org/2020/02/23/APT%20分析及%20TTPs%20提取/)



### 蓝队工具 fireeye

- [fireeye社區版](https://github.com/fireeye/commando-vm)
- [紅隊工具對抗](https://github.com/fireeye/red_team_tool_countermeasures)
    - 因爲泄露了工具，官方出了对抗得数据集


## AD域控

### 基本概念
- https://zhuanlan.zhihu.com/p/102694636

### 域控安全
- https://github.com/0Kee-Team/WatchAD/blob/master/README_zh-cn.md
- https://github.com/Integration-IT/Active-Directory-Exploitation-Cheat-Sheet
- [watchAD](https://github.com/0Kee-Team/WatchAD/blob/master/README_zh-cn.md)


### 搭建一些简单的环境进行试炼
- https://blog.csdn.net/xiaoi123/article/details/80167787
- https://www.sohu.com/a/242870169_750628
- [ZeroLogon 的利用以及分析(CVE-2020-1472)](https://www.anquanke.com/post/id/219374#h3-1)


### Bypass免杀（绕过和免杀相关的工具管理）
- pyloadallthings
- [BypassAntiVirus tide/免杀](https://github.com/TideSec/BypassAntiVirus)

