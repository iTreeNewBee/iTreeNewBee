---
layout: post
title:  "sublime自定义快捷键"
date:   2020-07-09 11:01:02
categories: software
tags: sublime
excerpt: sublime.log_commands(True)
---
* content
{:toc}

###找到需要修改的文件
点击 Preferences > Key Bindings, 此时会跳出一个新的sublime text窗口，窗口分为两部分，左边是默认的快捷键信息，右边是你自己设置的快捷键

###文件的大概介绍
观察可以看出，这个文本写的大致格式是
[
    {  "keys": ["快捷键"], "command": "快捷键对应的操作"},
    {......}
]
现在只需要知道自己所想要的快捷键以及对应的操作的名字就可以写出这样的语句。
要注意自己所设定的快捷键不应该与默认的快捷键冲突或者与系统快捷键冲突
###找到操作的名字
还是以 translate-CN 为例，首先要打开 sublime text 的控制台，可以使用快捷键 “ Ctrl + ` ” , 或者直接点击左下角的一个叫 switch panel 的小图标，然后点击 console 即可。
然后在控制台中输入命令
```sublime.log_commands(True)```
回车。从现在开始,你的所有动作的日志 (log) 都会被打印到控制台上。
此时开始使用一次translate-CN,每次操作的日志都被打印在了控制台上：
> command: drag_select {"event": {"button": 1, "x": 221.3, "y": 284.5}}
> command: context_menu {"event": {"button": 2, "x": 284.5, "y": 285.3}}
> command: translate_text {"event": {"x": 284.5, "y": 285.3}}

 从上到下依次对应“鼠标左键点击 / drag_select”，“鼠标右键点击 / context_menu”，“使用了translate的划词翻译功能 / translate_text”, 这里只需要记下最后一个操作即可，因为对 sublime text 自身来说，就算没有鼠标点击操作也同样可以使用翻译功能，故翻译功能之前的鼠标点击操作非必需 (但是需要选中一个词)。
所以知道 Translate-CN > current text 对应的 command 为 translate_text
同理知道 Translate-CN > input text 对应的 command 为 translate_input
tip: 要撤销刚才输入的让所有的操作日志都打印在控制台的操作，则向控制台输入命令：
```sublime.log_commands(False)```
###修改文件
 回到1中找到的文件，修改右边的部分，贴出我的作为参考
[
    { "keys": ["ctrl+t"], "command": "translate_text" },
    { "keys": ["ctrl+alt+t"], "command": "translate_input" }
]
要注意快捷键的设置不要和左边的那个文件有冲突，可以在左边查找 "ctrl+t" 看是否存在，以此来避免快捷键冲突
改完之后保存即可使用
