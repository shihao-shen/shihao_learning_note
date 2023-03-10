---
# 当前页面内容标题
title: ARP 协议
# sidebar: heading
# 当前页面图标
icon: note
# 分类
category:
    - 网络层
    - 协议
tag:
    - ARP
sticky: false
# 是否收藏在博客主题的文章列表中，当填入数字时，数字越大，排名越靠前。
star: false
# 是否将该文章添加至文章列表中
article: true
# 是否将该文章添加至时间线中
timeline: true
# sidebar: heading
order: 2
date: 2023-01-02
# 浏览量
pageview: true
---

# 📖 什么是ARP协议

ARP（Address Resolution Protocol）协议是用来将IP地址转换为物理地址的协议。物理地址指的是由硬件制造商分配给网络设备的唯一地址，也就是MAC地址。在TCP/IP协议族中，ARP协议是位于数据链路层和网络层之间的协议，它用于解决数据包在网络层传输的问题。



**为什么ARP是网络层?** 

在TCP/IP协议栈中，数据链路层负责在网络节点之间传输数据帧，而网络层负责路由转发数据包。ARP协议的作用就是在这两层之间桥接起来，使得网络层能够通过数据链路层来发送和接收数据。

因此，ARP协议并不属于数据链路层，而是属于网络层。

## 📑 ARP协议的结构

| 字段名                  | 字节 | 描述                          |
| ----------------------- | ---- | ----------------------------- |
| Hardware type           | 2    | 硬件类型                      |
| Protocol type           | 2    | 协议类型                      |
| Hardware length         | 1    | 硬件地址长度                  |
| Protocol length         | 1    | 协议地址长度                  |
| Operation               | 2    | 操作类型（请求或响应）        |
| Sender hardware address | 6    | 发送主机的硬件地址（MAC地址） |
| Sender protocol address | 4    | 发送主机的协议地址（IP地址）  |
| Target hardware address | 6    | 目标主机的硬件地址（MAC地址） |
| Target protocol address | 4    | 目标主机的协议地址（IP地址）  |

## 📑 ARP协议的工作原理

在计算机网络中，当一台主机想要与另一台主机通信时，它需要知道对方的IP地址和MAC地址。 IP地址是用于确定网络节点的位置的编号，而MAC地址是用于确定网络接口卡的位置的编号。

在一台主机想要发送数据到另一台主机时，它会使用ARP协议来查找对方的MAC地址。 它会在本地网络内广播一条ARP请求报文，其中包含了目标主机的IP地址。 所有的主机都会收到这条报文，但只有拥有指定IP地址的主机会回复一条ARP响应报文，其中包含了自己的IP地址和MAC地址。 发送数据的主机收到这条响应后，就会知道了对方的MAC地址，并可以开始通信。

以下是ARP工作流程的简单描述：

1. 主机A想要与主机B通信，但它不知道主机B的MAC地址。
2. 主机A广播一条ARP请求报文，其中包含了主机B的IP地址。
3. 所有的主机都会收到这条报文，但只有主机B会回复一条ARP响应报文。
4. 主机B回复的ARP响应报文中包含了自己的IP地址和MAC地址。
5. 主机A收到这条响应后，就会知道了主机B的MAC地址，并开始向主机B发送数据。
6. 主机B收到数据后，会回复一条确认报文，表示已经收到数据。

