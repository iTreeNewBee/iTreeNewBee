---
layout: post
title:  "Torshammer执行DDos攻击"
date:   2020-05-06 22:00:13
categories: DDos
tags: DDos 
excerpt: 测试服务安全性，根据最高院标准，服务器应该具备防御常见DDos攻击、icmp攻击，本节简单记录使用Torshammer对服务器进行DDos攻击测试。
---
* content
{:toc}  

## Torshammer

Torshammer使用python2.X编写，下载后有三个文件：socks.py、terminal.py、torshammer.py。只需要运行torshammer.py脚本。官网称可以通过单个实例杀死运行的Apache和IIS的大多数不受保护的web服务器。128个线程杀死Apache1.x和旧的IIS，使用256个线程杀死新的IIS和Apache2.x。

## 参数

* t 用于目标，某些域或者ip地址
* p 用于端口，默认值80
* r 线程数量
* T 代表定制攻击，挂代理使用方式  

## 使用方式

```
python .\torshammer.py -t 域\ip -p port -r number
```

