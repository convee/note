## tcpdump 简介：
    tcpdump是linux下的网络抓包工具。支持针对网络层，协议，主机，网络或者端口的过滤，并提供and or not等逻辑语句来去掉无用信息。
    
## 安装：

* ubuntu:
```
    $ sudo apt-get install tcpdump
```
* centos:
```
    $ yum install tcpdump
```
> tips: 如果安装失败，换一下国内的源即可，或者vpn下。

## 关键字：
* 类型关键字：host, net, port
* 传输方向的关键字：src, dst, dst or src, dst and src.这些 关键字指明了传输的方向。缺省是src or dst
* 协议的关键字：主要包括fddi, ip, arp, rarp, tcp, udp等类型。
* 其他关键字：gateway, broadcast, less, greater。
* 逻辑运算：!, ||, AND

查看可以监听的网络接口：

```
[root@iZuf69su1tsn6fy07g4262Z ~]# tcpdump -D
1.eth0 [Up, Running]
2.lo [Up, Running, Loopback]
3.any (Pseudo-device that captures on all interfaces) [Up, Running]
4.bluetooth-monitor (Bluetooth Linux Monitor) [none]
5.nflog (Linux netfilter log (NFLOG) interface) [none]
6.nfqueue (Linux netfilter queue (NFQUEUE) interface) [none]
7.usbmon0 (All USB buses) [none]
8.usbmon1 (USB bus number 1)
```


## tcpdump命令：

```
$ tcpdump option filter
    option: 选项
    filter: 过滤条件

$ tcpdump -Xnlps0 -nn -iany  host  192.168.5.1
  option: -Xnlps0 -nn -iany (选项)
  filter: host 192.168.5.1 (参数)
```

option:
    
-i [网络接口]： 监听哪个网络接口，默认监听的是-D显示的第一个网络接口。
    
-n：显示主机ip和端口。
    
-w [file]：把抓包的结果写入到file中。
    
-C [size(MB)]：配合-w使用，表示file大小，当抓包结果>size,自动生成新的文件。

-X：以16进制以及ASCII的形式打印出数据内容

-x：除了打印出header外，还打印packat中的数据

-xx：以16进制的形式打印header，packet里面的数据

-A: 把每一个packet都用ASCII的形式打印出来

-c：收到3个package就退出

-e：把连接层的头打印出来



filter:

1. 协议关键字：
    fddi, ip, arp, rarp
    
2. 源或目标主机：
    src, src or dst, src and dst


---
实例说明

本机环境说明：

PHP5.6 docke，ip为192.168.5.1

nginx  docker容器，ip为172.18.0.4

其他服务, ip为192.168.5.1

* 例子1： 访问本机一个页面，抓取数据包

```
xxxx@xxx:~/Documents$ sudo tcpdump -nn  host 192.168.5.1
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on br-ba99820d8dbf, link-type EN10MB (Ethernet), capture size 262144 bytes
10:54:04.448134 IP 172.18.0.4.37242 > 172.18.0.2.9000: Flags [S], seq 2092336432, win 29200, options [mss 1460,sackOK,TS val 43377964 ecr 0,nop,wscale 7], length 0

说明：
10:54:04.448134 IP：代表时间 和 数据包类型
172.18.0.4.37242 > 172.18.0.2.9000 表示数据包流向 
Flags[S(建立连接)|P(发送数据)|F(完成)|R(重置)|.(none)]
seq: 包序号
ack: 确认包
win: 数据窗口大小(接受窗口大小)
OPTIONS：tcp包 中的选项字段
MSS： 最大分段大小(发送数据的最大长度)
```

* 例子二：抓取整个请求到响应整个流程的包数据
```
xxxx@xxx:~/Documents$ tcpdump -nn  host 172.18.0.2 or 172.18.0.4
说明： 抓取php56 和 nginx两台docker的数据包
```

## 常用的几个抓包命令：

1. 获取指定IP上的所有请求，无包数据
```
$ tcpdump -nn host :IP
```

2. 获取指定IP上的所有请求，有包数据
```
$ tcpdump -nnX host :IP
```

3. 获取源IP发送到目的IP的所有包
```
$ tcpdump -nn src host :IP and \( dst host :IP and port :NUM \)
```

4. 获取 两个IP之间的相互通信
```
$ tcpdump -nn host :IP and host :IP
```

5. 获取IP发送了哪些包
```
$ tcpdump -nn src host :IP
```














