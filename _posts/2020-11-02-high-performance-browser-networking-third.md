---
layout: post
title: 《 Web 性能权威指南》阅读笔记 - 无线网络性能
date: 2020-11-02 17:56 +0800
tags: [阅读笔记, Network]
---

## 无线网络概览
### 无线网络的性能基础
所有无线技术都有自身的约束和局限。然而，无论使用哪种无线技术，所有通信方法都有一个最大的信道容量，这个容量是由相同的底层原理决定的。
香农公式：
![1872190F-4B8E-4CAE-AC4E-50EF1BF13AD5](https://raw.githubusercontent.com/dirtmelon/blog-images/main/1872190F-4B8E-4CAE-AC4E-50EF1BF13AD5.png)

- C 是信道容量，单位是 bit/s ；
- BW 是可用带宽，单位是 Hz ；
- S 是信号， N 是噪声，单位是 W 。
在所有这些因素中，与数据传输速度最直接相关的就是接收端与发送端之间的可用带宽和信号强度。

#### 带宽
有线网络通过线缆将网络中的各个节点连接起来，而无线电通信本质上则是一个共享媒体，它靠的是无线电波，或者专业一点讲，叫做电磁辐射。为实现通信，发送端与接收端必须事先就通信使用的频率范围达成共识，在这个频率范围内双方可以顺畅地交换信息。
除了以共有频段作为信息交互的基础外，影响性能的最主要因素就是频率范围的大小（带宽）。根据香农的模型，信道的总体比特率与分配的带宽呈正比。换句话说，在其他条件等同的情况下，频率范围加倍，传输速度加倍。

#### 信号强度
除了带宽之外，无线通信的第二个限制因素就是收发两端之间的信号强度，也叫信噪比（ SNR ， Signal Noise Ratio ）。本质上，信噪比衡量的是预期信号强度与背景噪声及干扰之间的比值。背景噪声越大，携带信息的信号就必须越强。

任何无线网络，无论它叫什么名字，缩写是什么或者修订版本是多少，其性能归根结底都受限于几个众所周知的因素。特别是分配给它的带宽大小和收发两端的信噪比。另外，所有利用无线电的通信都：通过共享的通信媒体（无线电波）实现；在管制下使用特定频率范围；在管制下使用特定的发射功率；受限于不断变化的背景噪声和干扰；受限于所选无线技术的技术约束；受限于设备本身的限制，比如形状、电源，等等。

### 测量现实中的无线性能
任何无线网络，无论它叫什么名字，缩写是什么或者修订版本是多少，其性能归根结底都受限于几个众所周知的因素。特别是分配给它的带宽大小和收发两端的信噪比。另外，所有利用无线电的通信都：
- 通过共享的通信媒体（无线电波）实现；
- 在管制下使用特定频率范围；
- 在管制下使用特定的发射功率；
- 受限于不断变化的背景噪声和干扰；
- 受限于所选无线技术的技术约束；
- 受限于设备本身的限制，比如形状、电源，等等。

## Wi-Fi
Wi-Fi 工作于免许可的ISM频段，任何人在任何地方都可以轻易部署，必要的硬件也很便宜很简单。

### 从以太网到无线局域网
802.11 无线标准主要是作为既有以太网标准（ 802.3 ）的扩展来设计的。事实上，以太网通常被称作局域网（ LAN ）标准，而802.11 标准族则相应地被称作无线局域网（ WLAN，Wireless LAN ）标准。
![5FA13F96-FF78-4D39-A229-0ED1BEDEE](https://raw.githubusercontent.com/dirtmelon/blog-images/main/5FA13F96-FF78-4D39-A229-0ED1BEDEEC86.png)

802.3 （以太网）和 802.11 (Wi-Fi) 的数据和物理层。

Wi-Fi 采用了冲突避免机制 （CSMA/CA ， Collision Avoidance ）机制，每个发送方都会在自己认为信道空闲时发送数据，以避免冲突。为此，每个Wi-Fi数据帧必须明确得到接收方的确认，以确保不发生冲突。

### Wi-Fi 性能与测量
Wi-Fi 标准没有规定任何中央调度机制，因而对任何客户端的吞吐量和延迟都不提供保证。
新的 WMM (Wi-Fi Multimedia ， Wi-Fi 多媒体）扩展支持在无线电接口中对需要的低延迟应用（语音，视频等）启用基本的 QoS (Quality of Service ，服务质量)，但是能识别的路由器和客户端都比较少，而且会和附近的 Wi-Fi 网络争用共享的无线资源，这是无法避免的。 Wi-Fi 网络之所以无处不在，主要原因就是它部署简单，而正因为部署简单，才会带来当前的性能问题。事实上，在城市繁华地段或者写字楼中，数十个 Wi-Fi 网络重叠的现象并不罕见：
![6A30C39D-0D7C-42F3-9E68-D7987B3E2499](https://raw.githubusercontent.com/dirtmelon/blog-images/main/6A30C39D-0D7C-42F3-9E68-D7987B3E2499.png)

2.4 GHz 和 5 GHz 的 Wi-Fi 重叠。
1. 多个 Wi-Fi 路由器共享带宽导致性能问题；
2. 从客户端到 Wi-Fi 接入点的第一跳需要多长时间没有保证；
如果你积极地采用新技术，那很可能显著提升 Wi-Fi 网络的性能。新的 802.11n 和 802.11ac 标准使用 5 GHz 频段，不仅拓宽了频率范围，而且能保证在多数环境下不发生冲突。 换句话说，至少在目前，如果你附近没有什么（像你一样的）技术大牛，那么一台双频路由器（支持 2.4GHz 和 5 GHz ）既能兼容 2.4 GHz 的老客户端，也能为支持 5 GHz 的客户端提供更好的性能。

Wi-Fi 性能的重要因素：
- 不保证用户的带宽和延迟时间；
- 信噪比不同，带宽也随之不同；
- 发射功率被限制在200 mW以内；
- i在2.4 GHz和较新的5 GHz频段中的频谱有限；
- 信道分配决定了接入点信号会重叠；
- 接入点与客户端争用同一个无线信道。

所有 Wi-Fi 协议的数据和物理层实现都有自己的重发和纠错机制，这些机制向上层隐藏了重发操作。
事实上，在 802.11n 之前， Wi-Fi 协议只允许同一时刻传输一个数据帧，这一帧必须得到链路层的确认才能继续发送下一帧。 802.11n 则引入了新的“帧聚合”功能，从而支持同时发送和确认多个 Wi-Fi 数据帧。除了直观的丢包问题， Wi-Fi 网络更突出的问题则是分组到达时间差异极大，这一切都要归咎于数据链路层和物理层的冲突及重发。

### 针对 Wi-Fi 的优化建议
多使用不计流量的宽带网络，而不是 3G/4G 
根据变化的带宽调整资源，如视频清晰度
适应可变的延迟时间，
有时候使用提供不可靠UDP传输的WebRTC倒不失为一个明智的选择。当然，传输方式的切换不能挽救无线网络，但却有助于降低协议和应用导致的延迟时间
## 移动网络
## G字号移动网络简介
每一代无线技术都以其峰值频谱效率（ bps/Hz ）为标志，为了让用户更直观地理解，这个效率会转换成数据传输速率，比如 4G 网络的传输速率以 Gbit/s 来衡量。
无论什么标准，每种网络真实的性能都会因提供商以及他们对网络的配置、每个小区内活跃用户的数量、特定位置的无线环境、使用的设备，以及影响无线性能的其他因素而异。

![382C4B1C-9958-418F-BCB5-ECCF6915B28A](https://raw.githubusercontent.com/dirtmelon/blog-images/main/382C4B1C-9958-418F-BCB5-ECCF6915B28A.png)

### 最早提供数据服务的 2G
1991年，芬兰基于新兴的 GSM （ Global System for Mobile communications ，全球移动通信系统）标准建设了第一个2G网络，最早在无线电网络中引入了数字信令。

直到1990年代中期，GPRS （ General Packet Radio Service ，通用无线分组业务）被引入 GSM 标准，无线互联网才真正走向实用。

### 3GPP 与 3GPP2
3GPP （ 3rd Generation Partnership Project ，第三代合作伙伴项目）负责制定 UMTS （ Universal Mobile TelecommunicationSystem ，通用移动通信系统），这是 3G 技术与 GSM 技术结合的产物。这个项目后来也负责维护 GSM 标准和制定新的LTE标准。
3GPP2 （ 3rd Generation Partnership Project 2 ）负责基于 CDMA2000 ，也就是高通制定的 IS-95 标准的后续技术制定 3G 规范
3G 网络存在两个主导且互不兼容的标准： UMTS 和 CDMA ，分别由 3GPP 和 3GPP2 制定。这两种标准同时也有自己的过渡性版本，通常被称为 3.5G， 3.75G 和 3.9G 。由于制定一个新标准需要很长时间，更重要的是，建设新网络需要巨额投资， 4G 的无线电接口及基础设备完全不同于 3G ，也为了很多购买了 3G 设备的用户的利益。因此 3GPP 和 3GPP2 一直在既有的 3G 标准基础上改进。

### 3G 技术演进
网络运营商和网络提供商一致认可 3GPP LTE 是各种网络共同的下一代4G标准。因此，很多 CDMA 网络运营商也率先投资建设了早期的 LTE 基础设施，以便在某种程度上保持对演进中的 HSPA+ 的竞争力。
换句话说，世界上的大多数移动运营商将把 HSPA+ 和 LTE 作为未来的移动无线标准。不用紧张，这应该是件好事。现有的 2G 和 3～3.75G 技术仍然是当前移动无线网络的主体，更重要的，它们至少还会继续为我们服务10年。
《Web 性能权威指南》写于 2013 年，现在是 2020 年，就中国地区来说 2G/3G 已经基本上被 4G 替代了， 5G 也在大力推广中。苹果也出了自己的第一代 5G手机— iPhone 12 。但是个人来说目前来说还看不到 5G 对于普通用户来说有多大的提升，或许等到 7 年以后又是另外一番景象吧。

### IMT-Advanced 的 4G 要求
4G 背后是一组具体要求（ IMT-Advanced ），这组要求是 ITU 在 2008 年就制定和公布了的。任何达到这些要求的技术，都可以看作是 4G 技术。 IMT-Advanced 的部分要求举例如下：
- 以 IP 分组交换网络为基础；
- 与之前的无线标准（ 3G 和 2G ）兼容；
- 移动客户端的速率达到 100 Mbit/s ，静止时的速率达到 Gbit/s 以上；
- 100 ms 控制面延迟， 10 ms 用户面延迟；
- 资源在用户间动态分配和共享；
- 可变带宽分配， 5～20 Mhz 。

### 长期演进（ LTE ）
LTE （ Long Term Evolution ）标准：
- 核心网络全部为 IP 分组交换网；
- 简化了网络架构，降低建设成本；
- 用户面和控制面的低延迟时间（分别为 <10 ms 和 <100 ms ）；
- 新无线接口及调制算法实现了高吞吐量（ 100Mbit/s ）；
- 可用于较大的带宽配置及运营商集群；要求所有设备支持 MIMO 。
由于其无线及核心网络的实现的差异， LTE 网络不是对已有 3G 基础设备的简单升级。相反， LTE 网络必须与现有 3G 基础设备并行部署，并采用不同的频率范围。不过，由于LTE是 UMTS 和 CDMA 的共同后继版本，因此它也提供了一种兼容二者的机制。由此， LTE 用户可以无缝切换到 3G 网络，并在 LTE 基础设施就绪后再迁移过来。

### 为多代并存的未来规划
首先，无线标准发展很快，但这些网络的物理设施建设则既要花钱又得花时间。将来，如果这些网络部署完成，那势必还要投入很多时间维护以收回成本，保证服务品质。换句话说，尽管市场上对 4G 的宣传炒作沸沸扬扬，老一代网络至少还得服务社会十年以上。所以，在创建移动 Web 应用时，应该考虑这一点。
在面向移动网络构建应用时，不能只考虑一种网络，更不能寄希望于特定的吞吐量或延迟时间。前面已经介绍过，任何网络的实际性能都具有高度可变性，取决于部署的版本、基础设施、无线条件，以及其他众多的因素。我们的应用要能适应不断变化的条件，吞吐量、延迟时间，甚至无线连接的有无，都可能变化。

## 设备特性及能力
经常被人忘记的一个事实，就是现有无线网络只是问题的一半。另一半当然是来自不同厂商的设备，以及它们的上市时间，这些设备各有各的特点。比如，CPU速度和核心数量、内存大小、存储能力、有无 GPU 等。这些因素中的任何一个都会影响设备以及运行于其上的应用的整体性能。

## 无线电资源控制器 （ RRC ）
3G和4G网络都有一个独特的装置，这个装置在有线网甚至Wi-Fi中都是不存在的。这个装置就是无线电资源控制器（RRC，Radio ResourceController ）。RRC负责调度协调移动设备与无线电基站之间所有的通信连接。 RRC 直接影响延迟、吞吐量和设备电池的使用时间。

![11E2E46B-AE45-47EF-8B50-398E2873F7E7](https://raw.githubusercontent.com/dirtmelon/blog-images/main/11E2E46B-AE45-47EF-8B50-398E2873F7E7.png)

## 移动网络的优化建议
### 节约用电
移动网络的性能与电池使用时间天生联系在一起。而且，为了节约用电，无线接口的物理层还专门针对如下限制（或事实）做出了优化：
- 全功率打开无线电模块只消几小时就可耗尽电量；
- 对无线电功率的需求随着无线标准演进与代俱增；
- 无线电模块的耗电量仅次于设备的屏幕；
- 数据传输时无线电通信的耗电过程是非线性的。
### 消除周期性及无效的数据
- 轮询在移动网络中代价极高，少用；
- 尽可能使用推送和通知；
- 出站和入站请求应该合并和汇总；
- 非关键性请求应该推迟到无线模块活动时进行；
- 消除不必要的长链接。
一般来说，推送比轮询效果更好。但频率过高的推送与轮询也不相上下。如果碰到实时更新的需求，应该考虑下列问题：
- 最佳更新间隔多长，是否符合用户预期？
- 除了固定的更新间隔，能否因地因时制宜？
- 入站或出站请求能否集合为更少的网络调用？
- 入站或出站请求能否推迟到以后发送？
### 预测网络延迟上限
在移动网络中，一个 HTTP 请求很可能会导致一连串长达几百甚至上几千毫秒的网络延迟。这一方面是因为有往返延迟，另一方面也不能忘记 DNS  、 TCP 、 TLS 及控制面的延迟。
一个 HTTP 请求的构成：

![DF4C61BD-6532-4A22-89A2-206FA99F1BFE](https://raw.githubusercontent.com/dirtmelon/blog-images/main/DF4C61BD-6532-4A22-89A2-206FA99F1BFE.png)

一个 HTTP 请求的延迟：

![4F7BD0AA-84FA-4D6F-8316-28B49B47C01A](https://raw.githubusercontent.com/dirtmelon/blog-images/main/4F7BD0AA-84FA-4D6F-8316-28B49B47C01A.png)

解耦用户交互与网络通信：
设计得好的应用，即便底层连接慢或者请求时间长，通过在UI中提供即时反馈也能让人觉得速度快。不要把用户交互与网络通信联系得太过紧密。为给用户最佳体验，应用必须在几百毫秒内响应输入。

### 面对多网络接口并存的现实
用户不喜欢速度慢的应用，但由于短暂网络错误导致的应用崩溃才是体验最差的。我们的移动应用必须足以应对各种常见的网络错误：无法访问的主机、吞吐量突然下降或延迟突然上升，甚至连接彻底断开。与有线网络不同，你不能假定一次连接成功就能持续保持连接状态。用户可能正在移动，可能进入了高冲突、用户多，或者信号差的区域。
- 不要缓存或试图猜测网络状态；
- 调度请求、监听并诊断错误；
- 瞬态错误总会发生，不可忽视，可以采取重试策略；
- 监听连接状态，以便采用最佳请求方式；
- 对重试请求采用补偿算法，不要永远循环；　
- 离线时，尽可能记录并在将来发送请求；
- 利用 HTML5 的 AppCache 和 localStorage 实现离线应用。

尽量使用 Wi-Fi 网络。

### 遵循协议和应用最佳实践。
网络基础设施的分层架构有一个最大的优点，那就是把物理交付接口从传输层中抽象了出来，而传输层又把路由和数据交付从应用协议中抽象了出来。这种分离的结果就是API具有独立性，但为了取得端到端的最佳性能，我们仍然要考虑整个架构。
通过重用持久连接、将服务器和数据部署到离客户端更近的地方、优化TLS部署，以及其他所有优化措施，对移动网络而言只会更加重要，因为移动网络的往返时间长，而带宽永远都很昂贵。

