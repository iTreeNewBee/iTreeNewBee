---
layout: post
title:  "软件测试实例"
date:   2020-05-27 21:00:01
categories: interview
tags: nk
excerpt: 测试用例如何编写实例问答演示
---
* content
{:toc}

### 给你一个字符串,怎么判断是不是ip地址?手写代码并写出测试用例.
ip格式:(1~255).(0~255).(0~255).(0~255)
方法一:正则表达式处理
```
import re
def check_ip(ipAddr):
  compile_ip=re.compile('^(1\d{2}|2[0-4]\d|25[0-5]|[1-9]\d|[1-9])\.(1\d{2}|2[0-4]\d|25[0-5]|[1-9]\d|\d)\.(1\d{2}|2[0-4]\d|25[0-5]|[1-9]\d|\d)\.(1\d{2}|2[0-4]\d|25[0-5]|[1-9]\d|\d)$')
  if compile_ip.match(ipAddr):
    return True  
  else:  
    return False
```
正则解释:
```
\d表示0~9的任何一个数字
{2}表示正好出现两次
[0-4]表示0~4的任何一个数字
| 的意思是或者
1\d{2}的意思就是100~199之间的任意一个数字
2[0-4]\d的意思是200~249之间的任意一个数字
25[0-5]的意思是250~255之间的任意一个数字
[1-9]\d的意思是10~99之间的任意一个数字
[1-9])的意思是1~9之间的任意一个数字
\.的意思是.点要转义（特殊字符类似，@都要加\\转义）
```
方法二:字符串拆解法
把ip地址当作字符串,以.为分隔符分割,进行判断
```
#!/usr/bin/python 
import os,sys 
def check_ip(ipAddr): 
    import sys 
    addr=ipAddr.strip().split('.') #切割IP地址为一个列表 
    #print addr 
    if len(addr) != 4: #切割后列表必须有4个参数 
        print "check ip address failed!"
        sys.exit() 
    for i in range(4): 
        try: 
            addr[i]=int(addr[i]) #每个参数必须为数字，否则校验失败 
        except: 
            print "check ip address failed!"
            sys.exit() 
        if addr[i]<=255 and addr[i]>=0:  #每个参数值必须在0-255之间 
            pass
        else: 
            print "check ip address failed!"
            sys.exit() 
        i+=1
    else: 
        print "check ip address success!"
if len(sys.argv)!=2: #传参加本身长度必须为2 
    print "Example: %s 10.0.0.1 "%sys.argv[0] 
    sys.exit() 
else: 
    check_ip(sys.argv[1]) #满足条件调用校验IP函数
```
方法三:引入IPy类库
```
import IPy 
 def is_ip(address): 
  try: 
    IPy.IP(address) 
    return True 
  except Exception as e: 
    return False
```
测试用例:
首先把IP地址分成有效可用的IP地址和有效但不可用的IP地址两个等价类;其中有效可用的IP地址包括IP地址的A,B,C三类地址,有效但不可用的IP地址包括D,E两类IP地址和A,B,C三类地址中的全网地址、广播地址、以及回环地址。


等价类划分 |
---- | ----
有效可用的IP地址
A类 | 1.0.0.0~126.255.255.254
A私有 | 10.0.0.0~10.255.255.254
B类 | 128.0.0.0~191.255.255.254
B私有 | 172.16.0.0~172.31.255.254
C类 | 192.0.0.0~223.255.255.254
C私有 | 192.168.0.0~192.169.255.254
windows自动分配 | 169.254.0.0~169.254.255.254
有效但不可用的IP地址 |
D类 | 244.0.0.0~239.255.255.254
E类 | 240.0.0.0~255.255.255.254
全网 | 0.x.x.x,x.x.x.0
广播 | x.x.x.255
回环 | 127.0.0.0~127.255.255.254
等


