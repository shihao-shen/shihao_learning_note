---
# 当前页面内容标题
title: UDP 协议
# sidebar: heading
# 当前页面图标
icon: note
# 分类
category:
    - 传输层
    - 协议
tag:
    - UDP
sticky: false
# 是否收藏在博客主题的文章列表中，当填入数字时，数字越大，排名越靠前。
star: false
# 是否将该文章添加至文章列表中
article: true
# 是否将该文章添加至时间线中
timeline: true
# sidebar: heading
order: 6
date: 2023-01-04
# 浏览量
pageview: true
---

# 📖 什么是UDP协议

UDP（User Datagram Protocol）是一种无连接的网络协议，它是基于IP协议的上一层协议。

UDP是一种面向数据报的协议，其主要功能是在两台计算机之间传输数据。 它与TCP（Transmission Control Protocol）相比，更加简单，但是也因此带来了一些缺陷，比如无法保证数据的可靠传输。

UDP的优势在于它的速度快，可以在要求实时性的应用中使用。 比如在视频会议、在线游戏等应用中，UDP协议都有着广泛的应用。

## 📑 字段结构

| 字段名           | 大小(比特) | 描述       |
| ---------------- | ---------- | ---------- |
| Source Port      | 16         | 源端口     |
| Destination Port | 16         | 目标端口   |
| Length           | 16         | 数据报长度 |
| Checksum         | 16         | 校验和     |
| Data             | Variable   | 数据       |

UDP数据报的最大长度为65507个字节，这是因为UDP头的长度固定为8个字节，加上数据的长度， 就得到了UDP数据报的总长度，也就是长度字段的值。长度字段的值是16位的，可以表示的最大值是65535。

但是UDP数据报的最大长度并不是65535个字节，而是65507个字节。这是因为在传输过程中，数据报可能会被分片， 分片后的每一个数据报都要在头部添加IP头。IP头长度固定为20个字节，因此实际上UDP数据报的最大长度为65535-20=65507个字节。

## 📑 工作原理	

当一台计算机使用UDP协议发送数据时，它会将数据封装成UDP数据报，并在数据报头部添加UDP头。 

| UDP报头 | 数据 |
| :-----: | :--: |

UDP头的长度固定为8个字节，因此UDP数据报的最大长度为65507个字节。

在发送UDP数据报之前，发送方会对UDP头和数据进行校验，并将校验和存储在UDP头的校验和字段中。 之后，UDP数据报就可以被发送出去了。

接收方收到UDP数据报后，会先检查目标端口是否正确。如果正确，就会对UDP头和数据进行校验，如果校验通过，则将数据从UDP数据报中提取出来， 交给上层协议进行处理。如果校验不通过，则丢弃数据报。

UDP协议的优点在于它比较简单，开销小，传输速度快。但是由于UDP是无连接的，无法保证数据的可靠传输， 所以在一些应用场景下并不适用。常见的应用场景包括多媒体流传输，在线游戏，实时数据传输等。	

## 📑 应用场景

UDP协议常用于以下场景：

- 要求实时性的应用，如视频会议、在线游戏等。
- 可以接受少量数据丢失的应用，如基于UDP的DNS协议。
- 对带宽的要求较低的应用，因为UDP协议的头部较短，带宽利用率较高。

## 📑 小结	

简单来说，UDP协议是一种无连接的网络协议，它可以快速地将数据从一台计算机发送到另一台计算机。 在传输过程中，UDP协议会在数据前面加上一个UDP头，并将数据封装成UDP数据报发送出去。 接收方收到UDP数据报后，会先检查目标端口是否正确，如果正确就将数据从UDP数据报中提取出来， 交给上层协议进行处理。由于UDP协议是无连接的，因此无法保证数据的可靠传输，但是在某些应用场景下仍然是一个不错的选择。