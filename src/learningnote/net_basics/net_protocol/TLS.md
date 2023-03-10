---
# 当前页面内容标题
title: TLS 协议
# sidebar: heading
# 当前页面图标
icon: note
# 分类
category:
    - 传输层
    - 协议
tag:
    - TLS
sticky: false
# 是否收藏在博客主题的文章列表中，当填入数字时，数字越大，排名越靠前。
star: false
# 是否将该文章添加至文章列表中
article: true
# 是否将该文章添加至时间线中
timeline: true
# sidebar: heading
order: 8
date: 2023-01-05
# 浏览量
pageview: true
---

# 📖 什么是 TLS 协议

SSL(Secure Sockets Layer)和TLS(Transport Layer Security)是两种用于在网络上传输数据的加密协议。它们的目的是在网络上传输数据时加密数据，使得只有拥有正确的解密密钥的接收者才能解密和读取数据。

SSL是最早的加密协议之一，被广泛应用于万维网上的数据传输。TLS是SSL的后继者，TLS 1.0是SSL 3.1的替代者。由于SSL的许多安全漏洞，许多组织和公司弃用了SSL并改用TLS。

TLS的概念和SSL非常相似，但是TLS在SSL的基础上进行了改进。TLS使用了更安全的密码算法和数学运算来保护数据，并且通过对安全机制的改进来增强了安全性。因此，TLS是当前使用最广泛的加密协议。

## 📑 协议结构

TLS协议在客户端和服务器之间建立一个安全的连接，并使用加密技术来保证数据的完整性和保密性。首先，客户端和服务器之间进行身份验证。然后，客户端和服务器使用密钥交换算法（如RSA或Diffie-Hellman）来协商加密密钥。最后，使用所协商的加密密钥对数据进行加密。

## 📑 工作原理

TLS协议的工作原理如下：

1. 客户端向服务器发起TLS握手请求。
2. 服务器返回TLS握手响应。
3. 客户端和服务器之间进行握手过程，建立一个安全的通信连接。
4. 客户端向服务器发送加密的数据。
5. 服务器收到加密的数据并解密。
6. 服务器处理请求并返回加密的响应。
7. 客户端收到加密的响应并解密。

### 📑 TLS的握手过程

TLS协议握手过程分为三个阶段：

1. 客户端发送"Client Hello"消息，包括客户端支持的加密套件、TLS协议版本以及一个随机数。
2. 服务端收到"Client Hello"消息后，回复"Server Hello"消息，包括服务端选择的加密套件、TLS协议版本以及一个随机数。
3. 客户端和服务端通过"Certificate"和"Server Hello Done"消息进行身份验证和密钥交换。

![TLS的握手过程](https://shihao-icu-1304033786.cos.ap-shanghai.myqcloud.com/shihao.icu/j2ubxgkzbm.png)

在这个过程中，双方都会使用对称加密和非对称加密来保证数据的安全性。非对称加密用于服务端向客户端发送证书，对称加密用于双方之间的通信。

总的来说，TLS的握手过程旨在确定双方使用的加密算法，并为之后的通信建立安全的通道。

## 📑 小结

TLS（Transport Layer Security，传输层安全协议）是一种用于在两个通信应用程序之间提供保密性和数据完整性的安全协议。它是对 SSL（Secure Sockets Layer，安全套接层）协议的改进版本，并且是目前互联网上使用最广泛的安全协议之一。