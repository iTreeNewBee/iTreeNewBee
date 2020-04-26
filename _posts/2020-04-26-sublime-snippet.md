---
layout: post
title:  "sublime设置snippet"
date:   2020-04-26 23:39:00
categories: sublime
tags: sublime
excerpt: sublime设置代码片段
---
* content
{:toc}

## 创建方法
Tools > New Snippet
然后你会看到
这时你会看到如下示例代码：
```
<snippet>
     <content><![CDATA[
Hello, ${1:this} is a ${2:snippet}.
]]></content>
     <!-- Optional: Set a tabTrigger to define how to trigger the snippet -->
     <!-- <tabTrigger>hello</tabTrigger> -->
     <!-- Optional: Set a scope to limit where the snippet will trigger -->
     <!-- <scope>source.python</scope> -->
</snippet>
```
## 说明
```
<snippet>
     <content><![CDATA[
        这里写你想要插入的代码段
]]></content>
    <!-- Optional: 在下一句中设置一个Tab触发键来触发你的触发器 -->
     <tabTrigger>这个就是任意设置的触发键</tabTrigger>
     <!-- Optional: 设置这个触发器的范围-->
     <scope>这里设置范围</scope>
</snippet>

```
## 使用
${1:name}表示代码插入后，光标所停留的位置，可同时插入多个。其中:name为自定义参数（可选）。
${2}表示代码插入后，按Tab键，光标会根据顺序跳转到相应位置（以此类推）。