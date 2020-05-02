---
layout: post
title:  "jekyll博客中markdown表格不显示"
date:   2020-05-02 09:39:49
categories: jekyll
tags: jekyll 
excerpt: 布局中增加代码显示markdown表格
---
* content
{:toc}  

将下面代码加入到_layouts对应的页面，显示markdown表格
```
<style>
  table{
    border-left:1px solid #000000;border-top:1px solid #000000;
    width: 100%;
    word-wrap:break-word; word-break:break-all;
  }
  table th{
  text-align:center;
  }
  table th,td{
    border-right:1px solid #000000;border-bottom:1px solid #000000;
  }
</style>

```