# 数据集 2021-12

## 1. NIMS 数据集（相较 2019 年 2021 年未发现变化）
网站地址：https://projects.cs.dal.ca/projectx/Download.html
NIMS 数据集由 Dalhousie 大学生成
分 NIMS1 data set，DARPA 1999 Week1 data set，DARPA 1999 Week3 data
set，MAWI dataset，NLANR (AMP) data set。
NIMS2 Data sets:包含有 GTALK，PRIMUS，ZFONE，ONLINE BANKING。ARFF/CSV
格式。作为研究 VoIp，不使用端口号，AMP 和 MAWI 没有 payload。
### 1.1 NIMS1 dataset
包含 6 种 SSH 服务流，来自 Internet，shell login，X11，local tunneling，
remote tunneling，SCP，SFTP，应用的协议 DNS，HTTP，FTP，P2P(limeware)。
### 1.2 NLANR (AMP) data set
包含 SSH 流
### 1.3 Anon17: Network Traffic Dataset of Anonymity Services
Anon17 数据收集于真实网络环境，带标注，3 种匿名服务数据，Tor，JonDonym，
I2P。包括的数据有 Tor，TorApp，TorPT，I2PApp80BW，I2PApp0BW，I2PUsers，
I2Papp，JonDonym。
### 1.4 NIMS lab botnet reseach data
包含 Zeus Botnet (Zeus-1),Citadel Botnet,Conficker Botnet,Alexa
(legitimate),Zeus Botnet (Zeus-2) 病毒数据包。
### 1.5 MAWI dataset
采样点 A-G，共 7 个采样点，收集历年的数据包，关于采样点的数据采样方
式的详细情况见http://mawi.wide.ad.jp/mawi/。



### 1.6 DARPA 数据集
DARPA 1999 年评测数据包括覆盖了 Probe，DoS，R2L，U2R 和 Data 等 5 大
类 58 种典型攻击方式，是目前最为全面的攻击测试数据集。同时，作为研究领
域共同认可及广泛使用的基准评测数据集，DARPA 1999 年评测数据为新提出的
入侵检测算法和技术与其他算法之间的比较提供了可能。DARPA 1999 评测数据
给出了 5 周的模拟数据，其中前两周是提供给参于评测者的训练数据：第 1，3
周为不包含任何攻击的正常数据；第 2 周中插入了属于 18 种类型的 43 次攻击
实例。后 2 周的数据则用于评测；第 4 周、第 5 周中包含了属于 58 种类型的
201 次攻击实例，其中 40 种攻击类型并没有在前两周的训练数据中出现，属于
新的攻击类型。

## 2. UNB 数据集
网站地址：https://www.unb.ca/cic/datasets/index.html
### 2.1 2019 年情况
UNB 数据恶意加密流数据集包括 CSE-CIC-IDS2018 on AWS，Intrusion
Detection Evaluation Dataset (CICIDS2017)，Intrusion Detection
Evaluation Dataset (CICIDS2012)，
CIC DoS dataset，VPN-nonVPN (ISCXVPN2016)，
Tor-nonTor dataset (ISCXTor2016)，Botnet dataset。
#### 2.1.1 CSE-CIC-IDS2018 on AWS
有 2 个方面，B-profile 在测试环境中产生良好的背景流量目的是为了能分
出用户的行为特征，包含一些网络事件， HTTPS, HTTP, SMTP, POP3, IMAP, SSH,
and FTP 应用协议；M-profile 包含 7 种不同攻击场景，有暴力破解，僵尸网络
病毒，Dos 攻击，DDos，Web Attacks 攻击。包含 Zeus，Are 2 种僵尸网络病毒，
在按键登陆时窃取银行账户信息和具有勒索性质的软件，Ares 病毒具有上传下
载文件等功能；其中的 SSH，HTTPS 属于加密流量；
M-profile: List of executed attacks and duration

![](/uploads/202201/uploads/datset/images/m_a1ad66619f22580ea7488981e8e760f0_r.png)

#### 2.1.2 Intrusion Detection Evaluation Dataset
(ISCXIDS2017)
覆盖的协议：HTTP, HTTPS, FTP, SSH, and email protocols.
攻击的类型：Web based, Brute force, DoS, DDoS, Infiltration, Heart-
bleed, Bot and Scan。
Day, Date, Description, Size (GB)
Monday, Normal Activity, 11.0G



Tuesday, attacks + Normal Activity, 11G
Wednesday, attacks + Normal Activity, 13G
Thursday, attacks + Normal Activity, 7.8G
Friday, attacks + Normal Activity, 8.3G
#### 2.1.3 Intrusion Detection Evaluation Dataset (ISCXIDS2012)
来自实验平台，覆盖的协议：HTTP, SMTP, SSH, IMAP, POP3, FTP
收集了 7 天数据，数据情况下如下：

- Friday, 11/6/2010, Normal Activity. No malicious activity, 16.1
- Saturday, 12/6/2010, Normal Activity. No malicious activity, 4.22
- Sunday, 13/6/2010, Infiltrating the network from inside + Normal Activity, 3.95
- Monday, 14/6/2010, HTTP Denial of Service + Normal Activity, 6.85
- Tuesday, 15/6/2010, Distributed Denial of Service using an IRC Botnet, 23.4
- Wednesday, 16/6/2010, Normal Activity. No malicious activity, 17.6
-  Thursday, 17/6/2010, Brute Force SSH + Normal Activity, 12.3

#### 2.1.4 VPN-nonVPN (ISCXVPN2016)
也称为 UNB ISCX Network Traffic 数据集，格式分 pcap 和 csv 2 种，包
含 14 种流量类型: VOIP, VPN-VOIP, P2P, VPN-P2P,HTTPS，SMTP/S,POP3/SSL,
IMAP/SSL,F TP over SSH (SFTP),FTP over SSL (FTPS)等，共 28GB。

![](/uploads/202201/uploads/datset/images/m_5f07ac0008f50b182dc1634892a36f5a_r.png)

Traffic: Content
Web Browsing: Firefox and Chrome
Email: SMPTS, POP3S and IMAPS
Chat: ICQ, AIM, Skype, Facebook and Hangouts
Streaming: Vimeo and Youtube
File Transfer: Skype, FTPS and SFTP using Filezilla and a external service
VoIP: Facebook, Skype and Hangouts voice calls (1h duration)
P2P: uTorrent and Transmission (Bittorrent)
工具

作用：pcap 格式转 csv 格式文件
名称：CICFlowMeter
官方项目地址：http://www.netflowmeter.ca/
github 地址：https://github.com/ISCX/CICFlowMeter
网上推荐使用地址：https://github.com/ronghuihu/CICFLOWMETER

#### 2.1.5 Tor-nonTor dataset (ISCXTor2016)

覆盖的协议：HTTP and HTTPS，SMTP/S，POP3/SSL，IMAP/SSL，FTP over SSH
(SFTP)，FTP over SSL (FTPS)，VoIP，P2P。
非洋葱网络流量采用 vpn 工程中的流量，洋葱网络流量有 7 种流量类型。一共
22GB。
#### 2.1.6 CTU-13 Dataset
- download: https://mcfp.felk.cvut.cz/publicDatasets/CTU-13-Dataset/CTU-13-Dataset.tar.bz2

- ref: https://blog.csdn.net/csdnliwenqi/article/details/116998353
- https://blog.51cto.com/u_15127660/3754447

CTU-13数据集。一个含有僵尸网络流量、正常流量和背景流量的且已标记的数据集。

CTU-13是2011年位于捷克共和国的捷克理工大学（CTU）捕获的僵尸网络流量数据集。数据集的目标是对混杂正常流量和背景流量的真实的僵尸网络流量进行大规模捕获。CTU-13数据集包含13个不同的僵尸网络样本捕获（也叫场景）。在每个场景我们执行一个特定的恶意软件，包括具有端口扫描，C&C 通信，攻击等行为的僵尸网络流量数据。它使用了某些协议并且执行了不同的操作。表2展示了僵尸网络场景的特征。

![](/uploads/202201/uploads/datset/images/m_93a4d1b1ea68a1d5a59c516fdf28eee0_r.png)


**Table 1. 僵尸网络场景的特征**

![](/uploads/202201/uploads/datset/images/m_a94a1ae4d13785245189c6008969b408_r.png)

**Table 2. 每一个僵尸网络场景下的数据统计**

每个场景捕获到一个pcap文件中，文件包含3种流量类型的数据包。对这些pcap文件进行处理来获取其他类型的信息，如NetFlows（单向网络流），WebLogs（网络日志），等等。对CTU-13数据集的第一次分析，在论文“An empirical comparison of botnet detection methods”中描述和发表。该论文用单向网络流来表示流量并且给流量赋予标签。单向网络流不应该被使用，因为我们第二篇数据集分析使用了双向网络流，效果超过了单向网络流。双向网络流与单向网络流相比有一些优点。首先，他们解决了区分客户端和服务器的问题；第二，他们包含了更多的信息。第三，他们包含更多详细的标签。使用双向网络流对数据集的第二个分析是在这里发布的。
场景的持续时间、数据包的数量、网络流的数量和pcap文件的大小，这些因素之间的关系如表3所示。这个表也展示了用于创建捕获文件的恶意软件和每个场景中感染的电脑数量。

![](/uploads/202201/uploads/datset/images/m_10806cbe1d2b71e74ee2309a07330e47_r.png)

**Table 3. 数据集中每个场景的网络流标签分布**

CTU-13数据集的独特之处是我们手动的分析和标记了每个场景。标记过程是在网络流文件中完成的。表4展示了每个场景中标记为“背景”、“僵尸网络”、“C&C通道”和“正常”标签的数量关系。

![](/uploads/202201/uploads/datset/images/m_fcef55f4bd723e89a98444ef2136a603_r.png)

#### 2.1.7 Botnet dataset

Botnet 数据集是 ISOT 数据集，ISCX 2012 IDS 数据集，Malware Capture Facility Project 数据集的混合。建立这个数据集的目的是为了评估僵尸网络病毒检测的准确率到一个可接受的程度。

ISOT 数据集包括 Waledac，Storm，Zeus 3 种不同的僵尸网络流量和一些背景流量(gaming packets, HTTP traffic and P2P bittorrent)；MalwareCapture Facility Project 中训练集有 4 种恶意流量，分别为 Neris, Rbot,Virut, and NSIS；测试集有 9 种恶意流量分别为 Neris, Rbot, Virut, NSIS,Menti, Sogou, and Murlo。

Botnet 测试集从 ISCX 2012 IDS 数据集采用了一部分正常的数据和部分
IRC 僵尸网络流量，训练集采用了 ISCX 2012 IDS 数据集的正常数据。

Botnet 训练集有 7 种僵尸网络流量，数据量 5.3G，其中 43.92%是恶意流量，其余是正常的流量;测试集数据有 16 种僵尸网络流量，数据量 8.5G，其中44.97%属于恶意流量。

##### 2.1.7.1 训练集流量类型分布情况
Botnet name | Type | Portion of flows in dataset
 --- | --- | --- 
Neris | IRC | 21159 (12%)
Rbot | IRC | 39316 (22%)
Virut | HTTP | 1638 (0.94 %)
NSIS | P2P | 4336 (2.48%)
SMTP Spam | P2P | 11296 (6.48%)
Zeus | P2P | 31 (0.01%)
Zeus control (C & C) | P2P | 20 (0.01%)

##### 2.1.7.2 测试集流量类型分布情况

Botnet name | Type | Portion of flows in dataset
 --- | --- | --- 
Neris | IRC | 25967 (5.67%)
Rbot | IRC | 83 (0.018%)
Menti | IRC | 2878(0.62%)
Sogou | HTTP | 89 (0.019%)
Murlo | IRC | 4881 (1.06%)
Virut | HTTP | 58576 (12.80%)
NSIS | P2P | 757 (0.165%)
Zeus | P2P | 502 (0.109%)
SMTP Spam | P2P | 21633 (4.72%)
UDP Storm | P2P | 44062 (9.63%)
Tbot | IRC | 1296 (0.283%)
Zero Access | P2P | 1011 (0.221%)
Weasel | P2P | 42313 (9.25%)
Smoke Bot | P2P | 78 (0.017%)
Zeus Control (C&C) | P2P | 31 (0.006%)
ISCX IRC bot | P2P | 1816 (0.387%)

### 2.2 2021 年更新情况：
#### 2.2.1 IDS 2018（原有，对应 2.1.1）
#### 2.2.2 IDS 2017（原有，对应 2.1.2）
#### 2.2.3 IDS 2012（原有，对应 2.1.3）
#### 2.2.4 VPN 2016（原有，对应 2.1.4）
#### 2.2.5 Tor 2016（原有，对应 2.1.5）
#### 2.2.6 Botnet 2014（原有，对应 2.1.7）
#### 2.2.7 CIC-Bell-DNS-EXF 2021

贝尔实验室 DNS 流量， 270.8 MB 的大型数据集。从 DNS 数据包中提取 30 个特
征，最终得到包含 323,698 个重攻击样本、53,978 个轻攻击样本和 641,642 个不同良性
样本的结构化数据集。
#### 2.2.8 CIC-Bell-DNS 2021
贝尔实验室 DNS 流量，其中包含 400,000 个良性和 13,011 个恶意样本，这些样本
是从公开可用数据集中的 100 万个良性域和 51,453 个已知恶意域中处理而来的。恶意
样本跨越三类垃圾邮件、网络钓鱼和恶意软件。我们的数据集 CIC-Bell-DNS2021 复制了
具有频繁良性流量和多种恶意域类型的真实场景。
#### 2.2.9 DNS over HTTPS (CIRA-CIC-DoHBrw2020)
DoH 流量样本。包括
- | -
  ---|---
  Non-DoH|通过访问使用 HTTPS 协议的网站产生的流量被捕获并标记为非 DoH 流量。为了捕获充足的流量以平衡数据集，浏览了来自 Alexa 域的数千个网站。
  良性 DoH|良性 DoH 是使用 Mozilla Firefox 和 Google Chrome Web 浏览器使用与非 DoH 中提到的相同技术生成的非恶意 DoH 流量。
  Malicious-DoH| DNS 隧道工具，例如 dns2tcp、DNSCat2 和 Iodine，用于生成恶意 DoH 流量。这些工具可以发送封装在 DNS 查询中的 TCP 流量。换句话说，这些工具创建了加密数据的隧道。因此，DNS 查询使用 TLS 加密的 HTTPS 请求发送到特殊的DoH 服务器。


#### 2.2.10 NSL-KDD dataset 2009
KDD'99 数据集的升级，包含的数据文件有：

KDDTrain+.ARFF：完整的 NSL-KDD 训练集，带有 ARFF 格式的二进制标签
KDDTrain+.TXT：完整的 NSL-KDD 训练集，包括 CSV 格式的攻击类型标签和难度级别
KDDTrain+_20Percent.ARFF：KDDTrain+.arff 文件的 20% 子集
KDDTrain+_20Percent.TXT：KDDTrain+.txt 文件的 20% 子集
KDDTest+.ARFF：完整的 NSL-KDD 测试集，带有 ARFF 格式的二进制标签
KDDTest+.TXT：完整的 NSL-KDD 测试集，包括 CSV 格式的攻击类型标签和难度级
别
KDDTest-21.ARFF：KDDTest+.arff 文件的子集，不包括难度级别为 21（共 21 个）
的记录
KDDTest-21.TXT：KDDTest+.txt 文件的子集，不包括难度级别为 21（共 21 个）的
记录
#### 2.2.11 CIC-DDoS 2019
DoS 攻击与来自 ISCX-IDS 数据集的无攻击痕迹混合在一起。我们用不同的工具制
作了 4 种类型的攻击，获得了 8 种不同的应用层 DoS 攻击痕迹。这些攻击针对的是 ISCX
数据集中的 10 个连接数最多的 Web 服务器。结果集包含 24 小时的网络流量，总大小
为 4.6 GB。
#### 2.2.12 DoS 2017
应用层 DoS 攻击与来自 ISCX-IDS 数据集的无攻击痕迹混合在一起。用不同的工具
制作了 4 种类型的攻击，获得了 8 种不同的应用层 DoS 攻击痕迹。这些攻击针对的是
ISCX 数据集中的 10 个连接数最多的 Web 服务器。结果集包含 24 小时的网络流量，
总大小为 4.6 GB。
#### 2.2.13 Darknet 2020
合并了之前生成的数据集，即 ISCXTor2016 和 ISCXVPN2016，并将各自的 VPN 和
Tor 流量合并到相应的暗网类别中。

#### 2.2.14 URL 2016
良性 URL：从 Alexa 顶级网站收集了超过 35,300 个良性 URL。这些域已经通过
Heritrix 网络爬虫来提取 URL。最初抓取了大约 50 万个唯一 URL，然后将其传递以删除
重复的和仅限域的 URL。后来提取的网址通过 Virustotal 进行检查，过滤出良性网址。
垃圾邮件 URL：从公开可用的 WEBSPAM-UK2007 数据集中收集了大约 12,000 个
垃圾邮件 URL。
网络钓鱼 URL：大约 10,000 个网络钓鱼 URL 来自 OpenPhish，它是一个活跃的网络钓鱼站点的存储库。
恶意软件 URL：从 DNS-BH 获得了超过 11,500 个与恶意软件网站相关的 URL，DNS-BH 是一个维护恶意软件站点列表的项目。
污损网址：超过 45,450 个网址属于污损网址类别。它们是 Alexa 排名受信任的网站，托管包含恶意网页的欺诈或隐藏 URL。
#### 2.2.15 CCCS-CIC-AndMal2020
包括 20 万个良性和 20 万个恶意软件样本，共计 40 万个 Android 应用程序，具有 14 个突出的恶意软件类别和 191 个突出的恶意软件家族。其中：
广告软件：1,253
银行业：2,100
短信恶意软件：3,904
风险软件：2,546
良性：1,795
总数：11,598
#### 2.2.16 CICMalDroid 2020
收集了超过 17,341 个 Android 样本，包括 VirusTotal 服务、Contagio 安全博客、
AMD、MalDozer 以及最近的研究贡献所使用的其他数据集。
#### 2.2.17 CICInvesAndMal2019
AndMal2017 数据集的第二部分。





#### 2.2.18 Android Malware Dataset (CIC-AndMal2017)
（原有，对应 6）
#### 2.2.19 Android Adware 2017(CIC-AAGM2017)（原有，
对应 5）
#### 2.2.20 安卓僵尸网络 2015
数据集包括 1929 个样本，生成时间为 2010 年（Android 僵尸网络的首次出现）到 2014 年。Android Botnet 数据集由 14 个家族组成：

Android Botnet 数据集由 14 个家族组成：
![](/uploads/202201/uploads/datset/images/m_4366552116d885345812e81e538213ec_r.png)

#### 2.2.21 Android Validation
由来自不同来源的 72 个原始应用程序组成，并在每个应用程序上进行了 10 次转换，从而产生了 792 个应用程序之间的不同关系


## 3. Malware Capture Facility Project Dataset

网站地址：https://www.stratosphereips.org/datasets-malware

### 3.1 2019 年情况

恶意软件的网络流量，有机构自己分析出来的恶意流量，包括网络文件，日
志，DNS 请求等，包含 340 个 malware pcap captures ？？？
The complete dataset can be found in the project web page.

![](/uploads/202201/uploads/datset/images/m_85b25d6a07233382bd3e6a391734cfb5_r.png)

### 3.2 2021 年情况
包括数据集，IPS，工程，工具。
#### 3.2.1 数据集
##### 3.2.1.1 CTU-13 DATASE T（原有，对应 2.1.6）
##### 3.2.1.2 MALWARE CAPTURES
蠕虫抓包数据，有 349 个文件。

##### 3.2.1.3 NORMAL CAPTURES
各种环境下抓取的正常通信数据包。具体如下：
- 1) CTU-Normal-4-only-DNS：从真实计算机正常捕获 DNS 流量。此捕获已减少到仅包括隐私问题的 DNS 流量。
- 2) CTU-Normal-5 ：普通用户（用户 A）在大学网络中的真实计算机中的正常捕获。用户有一个 Linux 操作系统并工作了几个小时。出于隐私原因，仅包含 binetflow
     流量。
- 3) CTU-Normal-6 ：普通用户（用户 B）在大学真实计算机中的正常捕获。用户有一
     个 Linux 操作系统并工作了几个小时。有几个包含网络日志和信息的文件，例如
     Bro. 出于隐私原因，pcap 文件被过滤为仅包含 DNS 数据包。
- 4) CTU-Normal-7 ：普通用户在家里的 Linux 笔记本中的普通 P2P 捕获。有几个文
     件，例如 pcap、weblogs 和 Bro 日志。
- 5) CTU-Normal-10 ：普通用户在 Windows 计算机中执行文件的正常捕获。有几个文 件 ， 例 如pcap 、 weblogs和Bro 日 志 。 (MD5 10a57a1ed06a26988a55d587662acf64)
- 6) CTU-Normal-12 ：普通捕获，特别是使用 P2P，从 xDSL 网络中的普通 Linux 笔
     记本电脑。有一些网页访问。
- 7) CTU-Normal-13 ：对网站 https://www.us.hsbc.com 的正常访问。与 CTU-281-1
     比较
- 8) CTU-Normal-20 ：Frantisek Strasak 为捕获 HTTPS 流量而进行的正常捕获。这次
     捕获是他 BruCon 谈话的一部分。
- 9) CTU-Normal-21 ：Frantisek Strasak 为捕获 HTTPS 流量而进行的正常捕获。这次
     捕获是他 BruCon 谈话的一部分。
- 10) CTU-Normal-22：Frantisek Strasak 为捕获 HTTPS 流量而进行的正常捕获。这次
      捕获是他 BruCon 谈话的一部分。
- 11) CTU-Normal-23：Frantisek Strasak 为捕获 HTTPS 流量而进行的正常捕获。这次
      捕获是他 BruCon 谈话的一部分。
- 12) CTU-Normal-24：Frantisek Strasak 为捕获 HTTPS 流量而进行的正常捕获。这次
      捕获是他 BruCon 谈话的一部分。
- 13) CTU-Normal-25：Frantisek Strasak 为捕获 HTTPS 流量而进行的正常捕获。这次
      捕获是他 BruCon 谈话的一部分。
- 14) CTU-Normal-26：Frantisek Strasak 为捕获 HTTPS 流量而进行的正常捕获。这次
      捕获是他 BruCon 谈话的一部分。
- 15) CTU-Normal-27：Frantisek Strasak 为捕获 HTTPS 流量而进行的正常捕获。这次
      捕获是他 BruCon 谈话的一部分。
- 16) CTU-Normal-28：Frantisek Strasak 为捕获 HTTPS 流量而进行的正常捕获。这次
      捕获是他 BruCon 谈话的一部分。
- 17) CTU-Normal-29：Frantisek Strasak 为捕获 HTTPS 流量而进行的正常捕获。这次
      捕获是他 BruCon 谈话的一部分。
- 18) CTU-Normal-30：Frantisek Strasak 为捕获 HTTPS 流量而进行的正常捕获。这次
      捕获是他 BruCon 谈话的一部分。
- 19) CTU-Normal-31：Frantisek Strasak 为捕获 HTTPS 流量而进行的正常捕获。这次捕获是他 BruCon 谈话的一部分。
- 20) CTU-Normal-32：Frantisek Strasak 为捕获 HTTPS 流量而进行的正常捕获。这次
      捕获是他 BruCon 谈话的一部分。
##### 3.2.1.4 MIXED CAPTURES
由长期恶意软件捕获、手动攻击、正常捕获和混合捕获组成的抓包数据。每个文件夹
中都有所捕获行为的描述。
1) CTU-Mixed-Capture-1 ：正常然后感染
2) CTU-Mixed-Capture-2 ：正常然后感染
3) CTU-Mixed-Capture-3 ：正常然后感染
4) CTU-Mixed-Capture-4 ：正常然后感染
5) CTU-Mixed-Capture-5 ：正常然后感染
##### 3.2.1.5 MALWARE ON IOT DATASE T
物联网数据集上的恶意软件抓包数据，具体如下：
![](/uploads/202201/uploads/datset/images/m_82c6e4cc0a433582fc6ea33a5126f72a_r.png)

##### 3.2.1.6 IOT-23 DATASET
带有恶意和良性物联网网络流量标记抓包数据集，包括：IoT-23 数据集 (21 GB)和仅包含标记文件 (8.8 GB) 的轻量型版本。

##### 3.2.1.7 ANDROID MISCHIEF DATASE T
来自感染了 Android RAT 的手机的网络流量数据集。包括：
1) RAT01 - ANDROID TESTER V.6.4.6
2) RAT02 - DROIDJACK V4.4
3) RAT03 - HAWKSHAW
4) RAT04 - SPYMAX V2.0
5) RAT05 - ANDRORAT
6) RAT06 - SAEFKO ATTACK SYSTEMS V4.9
7) RAT07 - AHMYTH
8) RAT08 - 命令行 ANDRORAT
##### 3.2.1.8 HORNET
Hornet 数据集整个 2021 年 4 月到 5 月从位于北美、欧洲和亚洲八个不同位置的八个相同配置的蜜罐服务器收集的。目前共有三个数据集：

- 1) Hornet 40：具有 2021 年 4 月、5 月和 6 月捕获的 40 天网络流量。
- 2) Hornet 15：在 2021 年 4 月和 5 月捕获了 15 天的网络流量。
- 3) Hornet 7：具有 2021 年 4 月捕获的 7 天网络流量。

#### 3.2.2 IPS
包括：linux 和 windows 版本 IPS，及测试框架。

#### 3.2.3 工具
包括：
1) Hexa Payload Decoder：在 C&C 服务器中自动提取和解码十六进制数据的工具。
2) Zeek Anomaly Detector：zeek/bro 的 conn.log 文件的异常检测器。
3) Zeek IRC Feature Extractor：基于 zeek 包的 IRC 特征提取器。
4) AIP Tool：实现 AIP 算法的开源工具。AIP 是一个行为分析引擎？？？

## 4. Dalhousie dataset（2021 年未查到）

采集了 8 小时的数据，来自 5 种应用 FTP，DNS，SSH，HTTP，MSN，有
12246 道流，6123 道流是 SSH，6123 道流是 non-SSH，SSH 通道的识别是建立在包头的识别，所以一共有 311130 个包，其中 157273 是 SSH 流包，153857 是非SSH 流包。

## 5. Android Adware and General Malware
Dataset
包含 20% 恶意的流量和 80%良性的流量包。

### 5.1. Adware (250 apps)
Airpush:用强制的广告来窃取用户信息。
Dowgin:广告库来窃取用户的信息。
Kemoge:接管用户的 Android 设备，这类广告是僵尸病毒的混合体通过把
自己包装成流行的 app。
Mobidash:通过展示广告的方式来窃取用户的信息。
Shuanet:跟 Kemoge 类似,Shuanet 也是接管用户设备。

### 5.2 .General Malware (150 apps)

AVpass:伪装成一个时钟 app。
FakeAV:设计成一种骗局，诱骗用户购买完整版本的软件，以便重新调解
不存在的感染。
FakeFlash/FakePlayer:设计成假 flash app 直接引导用户到网站上(在
成功安装后)。
GGtracker: 设计成短信的诈骗 (将短信息发送到保险费号码)完成用户
信息的窃取。
Penetho:设计成一种假的服务(hacktool 可以用来破解 WiFi 密码)。这
种病毒通过邮件附件，假更新,外部的媒体和感染的文档感染用户的电
脑。



## 6.Android
Malware
Dataset
(CICAndMal2017)
在真实手机上跑了恶意和良性的应用程序，4 种类别:
Adware
Ransomware
Scareware
SMS Malware
样本来自 42 种病毒家族，每种以及数量见下面:

### 6.1 Adware
Dowgin family, 10 captured samples
Ewind family, 10 captured samples
Feiwo family, 15 captured samples
Gooligan family, 14 captured samples
Kemoge family, 11 captured samples
koodous family, 10 captured samples
Mobidash family, 10 captured samples
Selfmite family, 4 captured samples
Shuanet family, 10 captured samples
Youmi family, 10 captured samples

### 6.2 Ransomware
Charger family, 10 captured samples
Jisut family, 10 captured samples
Koler family, 10 captured samples
LockerPin family, 10 captured samples
Simplocker family, 10 captured samples
Pletor family, 10 captured samples
PornDroid family, 10 captured samples
RansomBO family, 10 captured samples
Svpeng family, 11 captured samples
WannaLocker family, 10 captured samples



### 6.3 Scareware
AndroidDefender 17 captured samples
AndroidSpy.277 family, 6 captured samples
AV for Android family, 10 captured samples
AVpass family, 10 captured samples
FakeApp family, 10 captured samples
FakeApp.AL family, 11 captured samples
FakeAV family, 10 captured samples
FakeJobOffer family, 9 captured samples
FakeTaoBao family, 9 captured samples
Penetho family, 10 captured samples
VirusShield family, 10 captured samples
6.4 SMS Malware
BeanBot family, 9 captured samples
Biige family, 11 captured samples
FakeInst family, 10 captured samples
FakeMart family, 10 captured samples
FakeNotify family, 10 captured samples
Jifake family, 10 captured samples
Mazarbot family, 9 captured samples
Nandrobox family, 11 captured samples
Plankton family, 10 captured samples
SMSsniffer family, 9 captured samples
Zsone family, 10 captured samples
### 7.Italy Dataset（2021 年未查到）
收集了 96 小时，skype 的 VoIP 协议的网络包。
Data Start Time: 2006-05-29 10:01 CET
Data End Time: 2006-06-02 10:00 CET
Data Duration: 96 hours about



## 8. UNSW-NB15 Dataset （相较 2019 年无
变化）
网站地址：https://research.unsw.edu.au/projects/unsw-nb15-dataset
综合的现代攻击行为的混合体，这个数据集有 9 种类型的攻击，Fuzzers,
Analysis, Backdoors, DoS, Exploits, Generic, Reconnaissance, Shellcode
and Worms. The Argus, 使用了 Bro-IDS 工具，12 种算法设计产生 49 种特征
行为产生类别标签。涉及的协议类型SSH，SSHv2，BitTorrent。
## 9. Malware analysis blog data（新增数据至
2021 年，其他相较 2019 年无变化）
网站地址：https://www.malware-traffic-analysis.net/
采集了从 2013 年到 2019 年的病毒流量 pcap 数据。投放病毒者使用的文件
类型，病毒家族名称，MD5，病毒分析的年月日等。
包含 malspam-infection，fake flash，Js file download，Zeus Panda
Banker infection，Hookads，fake update，Netflix phish，ransomware malspam，
emotet infection with IcedID 等，涉及的加密协议有 TLSv1，TLSv1.2，SSL
等。
## 10. NETRESEC data（相较 2019 年无变化）
网站地址：https://www.netresec.com/?page=PcapFiles
包含 Citadel Botnet 等一些单个的包。采集来自蜜罐，沙箱和真实环境的
PCAP 包，类型分别为 APT，Crime，Metasplot，Trojan.Tbot，ZeroAccess Trojan，
CVE-2012-4681，Trojan Taidoor，Poison Ivy CnC，Shadowbrokers 等；数据中
包含的内容有投放病毒者使用的文件类型，病毒家族名称，MD5，病毒分析的年
月日等。有些病毒的文件和流量包来自 Malware analysis blog 数据集。
其中 CrypMic ransomware infection，Shadowbrokers 这些病毒流量中有加
密的流量。
## 11. ARCS 数据集
网站地址：https://csr.lanl.gov/data/

### 11.1 Unified Host and Network Data Set
大约 90 天内从洛斯阿拉莫斯国家实验室企业网络收集的网络和计算机（主
机）事件的子集。包括：Network Event Data 和 Host Event Data
### 11.2 Comprehensive, Multi-Source Cyber-Security Events
洛斯阿拉莫斯国家实验室公司内部计算机网络内的五个来源收集的连续 58
天的去标识化事件数据。包括：认证事件（auth.txt.gz）、过程（proc.txt.gz）、
流量（flows.txt.gz）、DNS(dns.txt.gz)、红队攻击事件（redteam.txt.gz）。
数据集总共压缩了大约 12 GB 的五类数据元素，并为 12,425 个用户、17,684台计算机和 62,974 个进程提供了总共 1,648,275,307 个事件。

## 12. 2017-SUEE 数据集
网站地址：https://hub.fastgit.org/vs-uulm/2017-SUEE-data-set
数据集包含进出乌尔姆大学电气工程学生会（Fachbereichsvertretung
Elektrotechnik）网络服务器的流量。这些数据集中包含的攻击是：50 名攻击
者运行 slowloris，50 个攻击者运行 slowhttptest，50 名攻击者运行slowloris-
ng。
Project Sonar 每个月都会生成多个 UDP 数据集。该数据是通过跨整个
IPv4 地址空间发送特定于协议的 UDP 探测来收集的。随着项目的成熟，每周发
送的探测类型继续扩大。
## 13. 物联网设置抓包数据
网 站 地 址 ： https://research.aalto.fi/en/datasets/iot-devices-
captures
设置 27 种不同类型的 31 个智能家居 IoT 设备期间发出的流量（4 种类
型分别由 2 个设备表示）。每个设备类型的每个设置至少重复 20 次。
## 14. Drebin 数据集
网站地址：https://www.sec.cs.tu-bs.de/~danarp/drebin/
该数据集包含来自 179 个不同恶意软件家族的 5,560 个应用程序。样本
是在 2010 年 8 月至 2012 年 10 月期间收集的。



## 15. PHP 安全漏洞数据集
网站地址：https://seam.cs.umd.edu/webvuldata/
包含三个 PHP Web 应用程序的多个版本的安全漏洞数据和计算的机器学习
功能：PHPMyAdmin、Moodle 和 Drupal。这些数据是为脆弱性预测研究收集的；然而，它也可以用于其他与预测无关的经验安全漏洞研究。该数据集中的所有漏洞都经过手动验证并定位到单个文件。

## 16. vizsec-IEEE

几个相关网站：

http://www.secrepo.com/
https://hub.fastgit.org/shramos/Awesome-Cybersecurity-Datasets
https://pcapr.net(未登录成功)
https://vizsec.org/

IEEE 网络安全可视化研讨会 (VizSec) 是一个论坛，汇集了来自学术界、
政府和行业的研究人员和从业人员，通过新的、有见地的可视化和分析技术满足
网络安全社区的需求。提供的可用数据集包括：

1) USB-IDS Datasets
2) Mordor Project
3) Advanced Research in Cyber System Data Sets
4) UNSW-NB15 Dataset
5) Canadian Institute for Cybersecurity’s Datasets
6) UGR’16
7) Stanford Large Network Dataset Collection (SNAP)
8) APTnotes
9) Darpa CGC (known vulnerabilities)
10) SoReL-20M Windows Portable Executable files
11) DNS data
12) SecRepo
13) malware-traffic-analysis
14) NETRESEC Data
15) CTU Data
16) Digital Corpora
17) Impact
18) Kyoto
19) The Honeynet Project
20) VAST Challenge 2013
21) VAST Challenge 2012
22) ORNL Auto-labeled corpus
23) Operationally Transparent Cyber (OpTC) Data

### 16.1 USB-IDS 数据集：
http://idsdata.ding.unisannio.it/
USB-IDS-1 由 17 个（压缩的）csv 文件组成，提供随时可用的标记网络流。

### 16.2 Mordor 项目：
https://mordordatasets.com/introduction.html
Mordor 项目以 JavaScript 对象表示法 (JSON) 文件的形式提供由模拟对抗技术生成的预先记录的安全事件，以便于使用。预先记录的数据按 Mitre ATT&CK 框架定义的平台、对手组、策略和技术进行分类。预先记录的数据不仅代表特定的已知恶意事件，还代表围绕它发生的其他上下文/事件。

### 16，3 网络系统数据集的高级研究：
https://csr.lanl.gov/data/
ARCS 提供从洛斯阿拉莫斯国家实验室企业网络收集的多个数据集。

### 16.4 NSW-NB15 数据集：
https://www.unsw.adfa.edu.au/unsw-canberra-cyber/cybersecurity/ADFA-NB15-Datasets/

UNSW-NB 15 数据集的原始网络数据包由澳大利亚网络安全中心 (ACCS) 网络靶场实验室的 IXIA PerfectStorm 工具创建，用于生成真实现代正常活动和合成当代的混合攻击行为。Tcpdump 工具用于捕获 100 GB 的原始流量（例如，Pcap 文件）。该数据集有九种攻击类型，分别是 Fuzzers、Analysis、Backdoors、DoS、Exploits、Generic、Reconnaissance、Shellcode 和 Worms。使用 Argus、Bro-IDS 工具并开发了 12 种算法，以生成总共 49 个具有类标签的特征。

下载链接：https://cloudstor.aarnet.edu.au/plus/index.php/s/2DhnLGDdEECo4ys
预估数据集大小：101.6G

### 16.5 加拿大网络安全研究所的数据集：
https://www.unb.ca/cic/datasets/index.html

加拿大网络安全研究所的数据集被世界各地的大学、私营企业和独立研究人员使用。有多个数据集可用。
进入数据集下载网站前需要输入参数的，只用在网址后面加上insert.php即可，不用输入任何参数。

下载链接 http://205.174.165.80/CICDataset/CICBellEXFDNS2021/insert.php
下载链接 http://205.174.165.80/CICDataset/CICBellDNS2021/insert.php
下载链接 http://205.174.165.80/CICDataset/CICAndMal2020/insert.php
下载链接 http://205.174.165.80/CICDataset/DoHBrw-2020/insert.php
下载链接 http://205.174.165.80/CICDataset/MalDroid-2020/insert.php
下载链接 http://205.174.165.80/CICDataset/CICDarknet2020/insert.php
下载链接 http://205.174.165.80/CICDataset/CICInvesAndMal2019/insert.php
下载链接 http://205.174.165.80/CICDataset/CICDDoS2019/insert.php
下载链接 http://205.174.165.80/CICDataset/CIC-IDS-2017/insert.php
下载链接 http://205.174.165.80/CICDataset/CICMalAnal2017/insert.php
下载链接 http://205.174.165.80/CICDataset/CICAndAdGMal2017/insert.php
下载链接 http://205.174.165.80/CICDataset/ISCX-SlowDoS-2016/insert.php
下载链接 http://205.174.165.80/CICDataset/ISCX-VPN-NonVPN-2016/insert.php
下载链接 http://205.174.165.80/CICDataset/ISCX-Tor-NonTor-2017/insert.php
下载链接 http://205.174.165.80/CICDataset/ISCX-URL-2016/insert.php
下载链接 http://205.174.165.80/CICDataset/ISCX-AndroidBot-2015/insert.php
下载链接 http://205.174.165.80/CICDataset/ISCX-Bot-2014/insert.php
下载链接 http://205.174.165.80/CICDataset/ISCX-AndroidValidation-2015/insert.php
下载链接 http://205.174.165.80/CICDataset/ISCX-IDS-2012/insert.php
下载链接 http://205.174.165.80/CICDataset/NSL-KDD/insert.php

预估数据集大小：88G

### 16.6 UGR'16: A New Dataset for the Evaluation of Cyclostationarity-Based Network IDSs 
https://nesg.ugr.es/nesg-ugr16

这里展示的数据集是用真实流量和最新攻击构建的。这些数据来自几个策略性地位于西班牙 ISP 网络中的 netflow v9 收集器。与以前的数据集相比，该数据集的主要优势在于它对评估考虑长期演变和流量周期性的 IDS 的有用性。考虑白天/晚上或工作日/周末劳动差异的模型也可以用它来训练和评估。

### 16.7 斯坦福大型网络数据集（SNAP)
不特定于安全性，但有几个相关的图形数据集。
https://snap.stanford.edu/data/index.html

### 16.8 APTnotes
https://github.com/aptnotes/data
APTnotes 是与供应商定义的 APT（高级持续威胁）组和/或工具集相关的恶意活动/活动/软件相关的公开论文和博客（按年份排序）的存储库。
下载链接 https://github.com/aptnotes/data
预估数据集大小：116M

### 16.9 Darpa CGC（已知漏洞）
https://github.com/CyberGrandChallenge/samples
网络框架漏洞挖掘挑战比赛。

下载链接：https://github.com/CyberGrandChallenge/samples
预估数据集大小：108M

### 16.10 SoReL-20M Windows 便携式可执行文件
下载链接 https://github.com/sophos-ai/SOREL-20M#a-note-on-dataset-size
预估数据集大小：8TB

### 16.11 DNS 数据
http://link.springer.com/chapter/10.1007/978-3-319-45719-2_9/fulltext.html
https://www.activednsproject.org/
发布链接和数据链接描述：超过 1 TB 的未处理 DNS PCAP 以及每天数十 GB 的重复数据删除 DNS 记录。因此，活跃的 DNS 数据集代表了世界日常 DNS 委托层次结构的重要部分。

### 16.12 SecRepo
是安全数据的精选列表。它包括恶意软件、NIDS、Modbus 和系统日志。它还包含许多以下链接。

下载链接 http://www.secrepo.com/
预估数据集大小：1.5G

### 16.13 恶意软件流量分析提供样本和 PCAP。(同 7)
http://www.malware-traffic-analysis.net/

它会逐日列出此处活跃的活动。

### 16.14 NETRESEC 数据：
https://www.netresec.com
公共数据包捕获存储库列表，可在 Internet 上免费获得。下面列出的大多数站点都共享完整数据包捕获 (FPC) 文件，但不幸的是，有些站点确实只有截断的帧。这包括 SCADA/ICS 网络捕获。

下载链接 https://www.netresec.com/?page=MACCDC
预估数据集大小：30G

下载链接 https://www.netresec.com/?page=ISTS
预估数据集大小：383G

下载链接: https://www.westpoint.edu/centers-and-research/cyber-research-center/data-sets
预估数据集大小：18M

下载链接 https://giantpanda.gtisc.gatech.edu/malrec/dataset/
预估数据集大小：3.5T

下载链接：https://download.netresec.com/pcap/FIRST-2015/NetworkForensics_VirtualBox.zip
数据集大小：5.8G

下载链接 ： https://download.netresec.com/pcap/FIRST-2015/FIRST-2015_Hands-on_Network_Forensics_PCAP.zip
数据集大小：4.4G

ACS_MILCOM_2016
下载链接 ：https://www.netresec.com/?page=ACS_MILCOM_2016
预估数据集大小：346G

UNSW-NB
下载链接 ： https://cloudstor.aarnet.edu.au/plus/index.php/s/2DhnLGDdEECo4ys?path=%2FUNSW-NB15%20-%20pcap%20files
数据集大小：99.2G

### 16.15 CTU-13 数据 （同 3.2.1.1 ）
https://stratosphereips.org/category/dataset.html
CTU-13 数据集包含一组在真实网络环境中完成的 13 种不同的恶意软件捕获。捕获包括僵尸网络、正常和后台流量。僵尸网络流量来自受感染的主机，正常流量来自已验证的正常主机，后台流量是我们不确定的所有其他流量。该数据集以逐流为基础进行标记，包含可用的最大和更多标记的僵尸网络数据集之一。

### 16.16 数字语料库：
http://digitalcorpora.org/
DigitalCorpora.org 是一个用于计算机取证教育研究的数字语料库网站。本网站上提供的所有磁盘映像、内存转储和网络数据包捕获均免费提供，无需事先授权或 IRB 批准即可使用。我们还提供从世界各地获取的真实数据的研究语料库。在特殊安排下可以使用该数据集。

### 16.17 impactcybertrust
http://www.impactcybertrust.org/
以前称为 PREDICT，即保护基础设施免受网络威胁的受保护存储库，是一个由安全相关网络操作数据的生产者和网络和信息安全研究人员组成的社区。该存储库为开发人员和评估人员提供与网络防御技术开发相关的定期更新的网络运营数据。数据集目录可公开访问，您无需登录即可浏览数据集详细信息。当前用户可以登录以请求数据集。

### 16.18 Kyoto
来自京都大学蜜罐的交通数据
http://www.takakura.com
下载链接 http://www.takakura.com/Kyoto_data/
预估数据集大小：33.5G

### 16.19 Honeynet 项目
http://honeynet.org/challenges
针对每个挑战的许多不同类型的数据，包括 pcap、恶意软件、日志。

### 16.20 VAST Challenge 2013 
http://vacommunity.org/VAST+Challenge+2013
Mini-challenge 3 与网络安全相关，包括网络流量数据、网络状态数据（通过大哥）和入侵防御系统数据。

### 16.21  VAST Challenge 2012
http://vacommunity.org/VAST+Challenge+2012
该挑战有两个小挑战，一个与态势感知相关（元数据和来自所有计算设备的定期状态报告），另一个与取证（防火墙和 IDS 日志）有关。

### 16.22 ORNL 自动标记语料库：
https://github.com/stucco/auto-labeled-corpus
网络安全领域中自动标记的文本数据的语料库。
下载链接 https://github.com/stucco/auto-labeled-corpus
预估数据集大小：4.8M

### 16.23 运营透明网络 (OptC) 数据：
来自约 500 个端点的端点活动以及来自企业出口点的 Zeek 数据。包括来自红队的良性记录生成和恶意软件注入。
https://github.com/FiveDirections/OpTC-data