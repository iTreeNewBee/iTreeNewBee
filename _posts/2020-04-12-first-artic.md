---
layout: post
title:  "markdown语法"
date:   2020-04-25 14:06:05
categories: rules
tags: markdown
excerpt: markdown语法规则简单介绍
---
* content
{:toc}

<p><strong>说明</strong>：现在markDown编译器和各平台支持情况都不太统一，为了达到一些效果会使用语法超集，但有些平台支持不好，请自行裁剪。简书使用的精简语法集合，文中有些语法效果显示不出来，为了发文的格式统一，同时也建议谨慎使用此类语法。</p>
<h2>一、概述</h2>
<h3>1.1 设计理念</h3>
<ul>
<li>Markdown 易于阅读，方便创作web文档，利于各平台无缝分发。</li>
<li>Markdown 语法灵感最大的来源还是纯文本 email 的格式，完全由标点符号标签组成的纯文本。</li>
<li>Markdown 文件应该以纯文本形式原样发布，不应该包含标记标签和格式化指令。</li>
</ul>
<h3>1.2 内联 HTML 语法</h3>
<ul>
<li>HTML 是一种<strong>发布格式</strong>，Markdown 是一种<strong>创作格式</strong>。</li>
<li>Markdown语法集合比较小，只是HTML标签的一小部分。</li>
<li>对于 Markdown 中未包含的标签, 可以直接使用 HTML标签，例如用 HTML <code>&lt;a&gt;</code> 标签替代 Markdown 的链接语法。</li>
</ul>
<h3>1.3 特殊字符自动转义</h3>
<p>  在 HTML 中, 有两个字符需要特殊对待: &lt; 和 &amp;，左尖括号用于起始标签。如果你想将它们用作字面量, 你必须将它们转义为字符实体, 例如<code>&amp;lt;</code> 和 <code>&amp;amp;</code>。</p>
<h2>二、行内语法讲解</h2>
<h3>2.1 注释的表述</h3>
<ul>
<li><strong>代码法</strong></li>
</ul>
<pre><code>&lt;div style='display: none'&gt;
哈哈我是注释，不会在浏览器中显示。
&lt;/div&gt;
</code></pre>
<ul>
<li><strong>html注释</strong></li>
</ul>
<p>既然支持html语法，那也支持html注释，快捷键 comment + /。</p>
<pre><code>&lt;!--哈哈我是注释，不会在浏览器中显示。--&gt;

&lt;!--
哈哈我是多段注释，
不会在浏览器中显示。
    --&gt;
</code></pre>
<ul>
<li><strong>hack方法</strong></li>
</ul>
<p>hack方法就是利用markdown的解析原理来实现注释的。<br>
一般有的markdown解析器不支持上面的注释方法，这个时候就可以用hack方法。<br>
hack方法比上面2种方法稳定得多，但是语义化太差。</p>
<pre><code>[//]: # (哈哈我是最强注释，不会在浏览器中显示。)
[^_^]: # (哈哈我是最萌注释，不会在浏览器中显示。)
[//]: &lt;&gt; (哈哈我是注释，不会在浏览器中显示。)
[comment]: &lt;&gt; (哈哈我是注释，不会在浏览器中显示。)
</code></pre>
<h3>2.2 分级标题、任务列表</h3>
<ul>
<li><strong>分级标题</strong></li>
</ul>
<pre><code># 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题  &lt;!--最多6级标题--&gt;
</code></pre>
<p>由于用了标记编辑器会把所有标题写到目录大纲中，在这里写的演示标题也会列进去，所以就不演示了。同学们自己在编辑器中观察，很简单，一级标题字号最大，依级递减。</p>
<ul>
<li><strong>任务列表</strong></li>
</ul>
<p>Markdown 语法：</p>
<pre><code>- [ ] 任务一 未做任务 `- + 空格 + [ ]`
- [x] 任务二 已做任务 `- + 空格 + [x]`
</code></pre>
<p>效果如下：</p>
<ul>
<li class="task-list-item"> 任务一 未做任务 <code>- + 空格 + [ ]</code>
</li>
<li class="task-list-item"> 任务二 已做任务 <code>- + 空格 + [x]</code>
</li>
</ul>
<h3>2.3 缩进、换行、空行、对齐方式</h3>
<ul>
<li><strong>首行缩进</strong></li>
</ul>
<p>不同特殊占位符所占空白是不一样大的。</p>
<pre><code>【1】 &amp;emsp;或&amp;#8195; //全角
【2】 &amp;ensp;或&amp;#8194; //半角
【3】 &amp;nbsp;或&amp;#160;  //半角之半角
</code></pre>
<ul>
<li><strong>换行</strong></li>
</ul>
<p>由于markdown编辑器的不同,可能在一行字后面，直接换行回车，也能实现换行，但是在Visual Studio Code上，想要<strong>换行必须得在一行字后面空两个格子才行</strong>。</p>
<ul>
<li><strong>空行</strong></li>
</ul>
<p>在编辑的时候有多少个空行(只要这一行只有回车或者space没有其他的字符就算空行)，在<strong>渲染之后，只隔着一行</strong>。</p>
<ul>
<li><strong>对齐方式</strong></li>
</ul>
<p>代码：</p>
<pre><code>&lt;center&gt;行中心对齐&lt;/center&gt;
&lt;p align="left"&gt;行左对齐&lt;/p&gt;
&lt;p align="right"&gt;行右对齐&lt;/p&gt;
</code></pre>
<p>显示效果：</p>
<p>&lt;center&gt;行中心对齐&lt;/center&gt;<br>
&lt;p align="left"&gt;行左对齐&lt;/p&gt;<br>
&lt;p align="right"&gt;行右对齐&lt;/p&gt;</p>
<h3>2.4 斜体、粗体、删除线、下划线、背景高亮</h3>
<ul>
<li>代码：</li>
</ul>
<pre><code>*斜体*或_斜体_
**粗体**
***加粗斜体***
~~删除线~~
++下划线++
==背景高亮==
</code></pre>
<ul>
<li>显示效果：</li>
</ul>
<p>  <em>斜体</em>    <strong>粗体</strong>   <strong><em>加粗斜体</em></strong>   <del>删除线</del>   ++删除线++   ==背景高亮==</p>
<h3>2.5 超链接、页内链接、自动链接、注脚</h3>
<ul>
<li><strong>行内式</strong></li>
</ul>
<p>语法说明：</p>
<p>[]里写链接文字，()里写链接地址, ()中的""中可以为链接指定title属性，title属性可加可不加。title属性的效果是鼠标悬停在链接上会出现指定的 title文字，链接地址与title前有一个空格。</p>
<p>代码：</p>
<pre><code>欢迎阅读 [择势勤](https://www.jianshu.com/u/16d77399d3a7 "择势勤")
</code></pre>
<p>显示效果：</p>
<p>欢迎阅读 <a href="https://www.jianshu.com/u/16d77399d3a7" target="_blank">择势勤</a></p>
<ul>
<li><strong>参考式</strong></li>
</ul>
<p>参考式超链接一般用在学术论文上面，或者另一种情况，如果某一个链接在文章中多处使用，那么使用引用 的方式创建链接将非常好，它可以让你对链接进行统一的管理。</p>
<p>语法说明：<br>
参考式链接分为两部分，文中的写法 [链接文字][链接标记]，在文本的任意位置添加[链接标记]:链接地址。</p>
<p>如果链接文字本身可以做为链接标记，你也可以写成[链接文字][]<br>
[链接文字]：链接地址的形式，见代码的最后一行。</p>
<p>代码：</p>
<pre><code>我经常去的几个网站[Google][1]、[Leanote][2]。

[1]:http://www.google.com 
[2]:http://www.leanote.com
</code></pre>
<p>显示效果：</p>
<p>我经常去的几个网站<a href="https://links.jianshu.com/go?to=http%3A%2F%2Fwww.google.com" target="_blank">Google</a>、<a href="https://links.jianshu.com/go?to=http%3A%2F%2Fwww.leanote.com" target="_blank">Leanote</a>。</p>
<ul>
<li><strong>注脚</strong></li>
</ul>
<p>语法说明：</p>
<p>在需要添加注脚的文字后加上脚注名字[^注脚名字],称为加注。 然后在文本的任意位置(一般在最后)添加脚注，脚注前必须有对应的脚注名字。</p>
<p>注意：经测试注脚与注脚之间必须空一行，不然会失效。成功后会发现，即使你没有把注脚写在文末，经Markdown转换后，也会自动归类到文章的最后。</p>
<p>代码：</p>
<pre><code>使用 Markdown[^1]可以效率的书写文档, 直接转换成 HTML[^2]。

[^1]:Markdown是一种纯文本标记语言

[^2]:HyperText Markup Language 超文本标记语言
</code></pre>
<p>显示效果：</p>
<p>使用 Markdown<sup><a href="#fn1" id="fnref1">[1]</a></sup>可以效率的书写文档, 直接转换成 HTML<sup><a href="#fn2" id="fnref2">[2]</a></sup>。</p>
<p>注：脚注自动被搬运到最后面，请到文章末尾查看，脚注后方的链接可以直接跳转回到加注的地方。</p>
<ul>
<li><strong>锚点（页内超链接）</strong></li>
</ul>
<p>网页中，锚点其实就是页内超链接，也就是链接本文档内部的某些元素，实现当前页面中的跳转。比如我这里写下一个锚点，点击回到目录，就能跳转到目录。 在目录中点击这一节，就能跳过来。还有下一节的注脚。这些根本上都是用锚点来实现的，只支持在标题后插入锚点，其它地方无效。</p>
<p>代码：</p>
<pre><code>## 0. 目录{#index}
</code></pre>
<p>显示效果：</p>
<p>跳转到<a href="#index" target="_blank">目录</a></p>
<ul>
<li><strong>自动链接</strong></li>
</ul>
<p>语法说明：<br>
Markdown 支持以比较简短的自动链接形式来处理网址和电子邮件信箱，只要是用&lt;&gt;包起来， Markdown 就会自动把它转成链接。一般网址的链接文字就和链接地址一样，例如：</p>
<p>代码：</p>
<pre><code>&amp;lt;http://example.com/&amp;gt; &amp;emsp;&amp;emsp; 
&amp;lt;address@example.com&amp;gt;
</code></pre>
<p>显示效果：</p>
<p>&lt;<a href="https://links.jianshu.com/go?to=http%3A%2F%2Fexample.com%2F" target="_blank">http://example.com/</a>&gt;   <br>
&lt;<a href="https://links.jianshu.com/go?to=mailto%3Aaddress%40example.com" target="_blank">address@example.com</a>&gt;</p>
<h3>2.6 无序列表、有序列表、定义型列表</h3>
<ul>
<li>
<strong>无序列表</strong>  <br>
使用 *，+，- 表示无序列表。<br>
代码：</li>
</ul>
<pre><code>* 无序列表项 一
+ 无序列表项 二
- 无序列表项 三
</code></pre>
<p>显示效果：</p>
<ul>
<li>无序列表项 一</li>
</ul>
<ul>
<li>无序列表项 二</li>
</ul>
<ul>
<li>无序列表项 三</li>
</ul>
<ul>
<li><strong>有序列表</strong></li>
</ul>
<p>有序列表则使用数字接着一个英文句点。<br>
代码：</p>
<pre><code>1. 有序列表项 一
2. 有序列表项 二
3. 有序列表项 三
</code></pre>
<p>显示效果：</p>
<ol>
<li>有序列表项 一</li>
<li>有序列表项 二</li>
<li>有序列表项 三</li>
</ol>
<ul>
<li><strong>定义型列表表</strong></li>
</ul>
<p>语法说明：</p>
<blockquote>
<p>定义型列表由名词和解释组成。一行写上定义，紧跟一行写上解释。解释的写法:紧跟一个缩进(Tab)</p>
</blockquote>
<p>代码</p>
<pre><code>:   轻量级文本标记语言（左侧有一个可见的冒号和四个不可见的空格）
</code></pre>
<p>显示效果：</p>
<p>Markdown<br>
:   轻量级文本标记语言，可以转换成html，pdf等格式</p>
<h3>2.7 插入图像</h3>
<p>语法中图片Alt的意思是如果图片因为某些原因不能显示，就用定义的图片Alt文字来代替图片。 图片Title则和链接中的Title一样，表示鼠标悬停与图片上时出现的文字。 Alt 和 Title 都不是必须的，可以省略，但建议写上。</p>
<p>Markdown 语法：</p>
<pre><code>&lt;center&gt;  &lt;!--开始居中对齐--&gt;

![GitHub set up](http://zh.mweb.im/asset/img/set-up-git.gif "图片Title")
格式: ![图片Alt](图片地址 "图片Title")
&lt;/center&gt; &lt;!--结束居中对齐--&gt;
</code></pre>
<p>效果如下：</p>
<br>
<div class="image-package">
<div class="image-container" style="max-width: 310px; max-height: 250px;">
<div class="image-container-fill" style="padding-bottom: 80.65%;"></div>
<div class="image-view" data-width="310" data-height="250"><img data-original-src="//upload-images.jianshu.io/upload_images/1496626-c3d52ee452341b61.png" data-original-width="310" data-original-height="250" data-original-format="image/png" data-original-filesize="22473"></div>
</div>
<div class="image-caption">GitHub set up</div>
</div>
<h3>2.8 多级引用</h3>
<p>语法说明：</p>
<p>引用需要在被引用的文本前加上&gt;符号和空格，允许多层嵌套，也允许你偷懒只在整个段落的第一行最前面加上 &gt; 。</p>
<p>代码：</p>
<pre><code>&gt;&gt;&gt; 请问 Markdwon 怎么用？ - 小白
&gt;&gt; 自己看教程！ - 愤青
&gt; 教程在哪？ - 小白
</code></pre>
<p>显示效果：</p>
<blockquote>
<blockquote>
<blockquote>
<p>请问 Markdwon 怎么用？ - 小白</p>
</blockquote>
</blockquote>
</blockquote>
<blockquote>
<blockquote>
<p>自己看教程！ - 愤青</p>
</blockquote>
</blockquote>
<blockquote>
<p>教程在哪？ - 小白</p>
</blockquote>
<h3>2.9 转义字符、字体、字号、颜色</h3>
<ul>
<li><strong>转义字符</strong></li>
</ul>
<p>Markdown中的转义字符为\，转义的有：</p>
<p>\ 反斜杠 ` 反引号 * 星号 _ 下划线 {} 大括号 [] 中括号 () 小括号  # 井号 + 加号 - 减号 . 英文句号 ! 感叹号</p>
<ul>
<li><strong>字体、字号、颜色</strong></li>
</ul>
<p>代码：</p>
<pre><code>&lt;font face="黑体"&gt;我是黑体字&lt;/font&gt;
&lt;font face="微软雅黑"&gt;我是微软雅黑&lt;/font&gt;
&lt;font face="STCAIYUN"&gt;我是华文彩云&lt;/font&gt;
&lt;font color=#0099ff size=12 face="黑体"&gt;黑体&lt;/font&gt;
&lt;font color=gray size=5&gt;gray&lt;/font&gt;
&lt;font color=#00ffff size=3&gt;null&lt;/font&gt;
</code></pre>
<p>显示效果：</p>
<p>&lt;font face="黑体"&gt;我是黑体字&lt;/font&gt;<br>
&lt;font face="微软雅黑"&gt;我是微软雅黑&lt;/font&gt;<br>
&lt;font face="STCAIYUN"&gt;我是华文彩云&lt;/font&gt;<br>
&lt;font color=#0099ff size=12 face="黑体"&gt;黑体&lt;/font&gt;<br>
&lt;font color=gray size=5&gt;gray&lt;/font&gt;<br>
&lt;font color=#00ffff size=3&gt;null&lt;/font&gt;</p>
<h2>三、块语法讲解</h2>
<h3>3.1 内容目录</h3>
<p>在段落中填写 [TOC] 以显示全文内容的目录结构。</p>
<pre><code>[TOC]
</code></pre>
<p>效果参见最上方的目录。</p>
<h3>3.2 代码块</h3>
<p>对于程序员来说这个功能是必不可少的，插入程序代码的方式有两种，一种是利用缩进(Tab), 另一种是利用”`”符号（一般在ESC键下方）包裹代码。</p>
<ul>
<li><strong>行内式</strong></li>
</ul>
<p>代码：</p>
<pre><code>C语言里的函数 `scanf()` 怎么使用？
</code></pre>
<p>显示效果：</p>
<p>C语言里的函数 <code>scanf()</code> 怎么使用？</p>
<ul>
<li><strong>缩进式多行代码</strong></li>
</ul>
<p>缩进 4 个空格或是 1 个制表符</p>
<p>一个代码区块会一直持续到没有缩进的那一行（或是文件结尾）。</p>
<p>代码：</p>
<pre><code>#include &amp;lt;stdio.h&amp;gt;
int main(void)
{
    printf(&amp;#34;Hello world\n&amp;#34;);
}
</code></pre>
<p>显示效果：</p>
<pre><code>#include &amp;lt;stdio.h&amp;gt;
int main(void)
{
    printf(&amp;#34;Hello world\n&amp;#34;);
}
</code></pre>
<ul>
<li><strong>用六个`包裹多行代码</strong></li>
</ul>
<p>代码：</p>
<pre><code>、、、
include &lt;stdio.h&gt;
int main(void)
{
printf("Hello world\n");
}
、、、
</code></pre>
<p><strong>显示效果：</strong></p>
<pre><code>include &lt;stdio.h&gt;
int main(void)
{
printf("Hello world\n");
}
</code></pre>
<h3>3.3 流程图</h3>
<p>编辑自有道云笔记，代码：</p>
<pre><code>```
graph LR
A--&gt;B
```

```
sequenceDiagram
A-&gt;&gt;B: How are you?
B-&gt;&gt;A: Great!
```
</code></pre>
<p>显示效果：</p>
<pre><code>graph LR
A--&gt;B
</code></pre>
<pre><code>sequenceDiagram
A-&gt;&gt;B: How are you?
B-&gt;&gt;A: Great!
</code></pre>
<h3>3.4 表格</h3>
<p>语法说明：</p>
<p>不管是哪种方式，第一行为表头，第二行分隔表头和主体部分，第三行开始每一行为一个表格行。<br>
列于列之间用管道符|隔开。原生方式的表格每一行的两边也要有管道符。<br>
第二行还可以为不同的列指定对齐方向。默认为左对齐，在-右边加上:就右对齐。<br>
<code>-</code> 左对齐， <code>:-:</code> 中心对齐，<code>-:</code> 右对齐</p>
<p>表格代码：</p>
<pre><code>|学号|姓名|序号|
|-|-|-|
|小明明|男|5|
|小红|女|79|
|小陆|男|192|
</code></pre>
<p>原生方式写表格：<br>
&lt;center&gt;</p>
<table>
<thead>
<tr>
<th>学号</th>
<th style="text-align:center">姓名</th>
<th style="text-align:right">序号</th>
</tr>
</thead>
<tbody>
<tr>
<td>小明明</td>
<td style="text-align:center">男</td>
<td style="text-align:right">5</td>
</tr>
<tr>
<td>小红</td>
<td style="text-align:center">女</td>
<td style="text-align:right">79</td>
</tr>
<tr>
<td>小陆</td>
<td style="text-align:center">男</td>
<td style="text-align:right">192</td>
</tr>
</tbody>
</table>
<p>&lt;/center&gt;</p>
<h3>3.5 LaTeX 公式</h3>
<ul>
<li><strong>表示行内公式</strong></li>
</ul>
<p>代码：</p>
<pre><code>质能守恒方程可以用一个很简洁的方程式 `$E = m c^2 $`来表达。
</code></pre>
<p>显示效果：</p>
<p>质能守恒方程可以用一个很简洁的方程式 <code>$E = m c^2 $</code>来表达。</p>
<ul>
<li>
<strong>表示整行公式</strong><br>
大部分的浏览器支持的</li>
</ul>
<pre><code>$$ 公式 $$
</code></pre>
<p>有道云笔记 使用格式，</p>
<pre><code>```math
E = mc^2
```
</code></pre>
<p>块级公式：</p>
<pre><code>```math
x = \dfrac{-b \pm \sqrt{b^2 - 4ac}}{2a} 
```
```math
[\frac{1}{\Bigl(\sqrt{\phi \sqrt{5}}-\phi\Bigr) e^{\frac25 \pi}} =
1+\frac{e^{-2\pi}} {1+\frac{e^{-4\pi}} {1+\frac{e^{-6\pi}}
{1+\frac{e^{-8\pi}} {1+\ldots} } } }]

```
</code></pre>
<p>显示效果：</p>
<pre><code class="math">x = \dfrac{-b \pm \sqrt{b^2 - 4ac}}{2a} 
</code></pre>
<pre><code class="math">[\frac{1}{\Bigl(\sqrt{\phi \sqrt{5}}-\phi\Bigr) e^{\frac25 \pi}} =
1+\frac{e^{-2\pi}} {1+\frac{e^{-4\pi}} {1+\frac{e^{-6\pi}}
{1+\frac{e^{-8\pi}} {1+\ldots} } } }]

</code></pre>
<p>访问 <a href="https://links.jianshu.com/go?to=https%3A%2F%2Fmath.meta.stackexchange.com%2Fquestions%2F5020%2Fmathjax-basic-tutorial-and-quick-reference" target="_blank">MathJax</a> 参考更多使用方法。</p>
<h3>3.6 分隔线</h3>
<p>你可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格。下面每种写法都可以建立分隔线：</p>
<p>代码：</p>
<pre><code>* * *
***
*****
- - -
-----------
</code></pre>
<p>显示效果都一样：</p>
<hr>
<hr>
<hr>
<hr>
<hr>
<h3>3.7 HTML 原始码</h3>
<p>在代码区块里面， &amp; 、 &lt; 和 &gt; 会自动转成 HTML 实体，这样的方式让你非常容易使用 Markdown 插入范例用的 HTML 原始码，只需要复制贴上，剩下的 Markdown 都会帮你处理，例如：</p>
<p><strong>代码：</strong></p>
<pre><code>第一个例子：
&lt;div class="footer"&gt;
© 2004 Foo Corporation
&lt;/div&gt;
第二个例子：
&lt;center&gt;

&lt;table&gt;
&lt;tr&gt;
&lt;th rowspan="2"&gt;值班人员&lt;/th&gt;
&lt;th&gt;星期一&lt;/th&gt;
&lt;th&gt;星期二&lt;/th&gt;
&lt;th&gt;星期三&lt;/th&gt;
&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;李强&lt;/td&gt;
&lt;td&gt;张明&lt;/td&gt;
&lt;td&gt;王平&lt;/td&gt;
&lt;/tr&gt;
&lt;/table&gt;

&lt;/center&gt;
</code></pre>
<p>显示效果：</p>
<p>第一个例子：<br>
&lt;div class="footer"&gt;<br>
© 2004 Foo Corporation<br>
&lt;/div&gt;</p>
<p>第二个例子：</p>
<p>&lt;center&gt;</p>
<p>&lt;table&gt;<br>
&lt;tr&gt;<br>
&lt;th rowspan="2"&gt;值班人员&lt;/th&gt;<br>
&lt;th&gt;星期一&lt;/th&gt;<br>
&lt;th&gt;星期二&lt;/th&gt;<br>
&lt;th&gt;星期三&lt;/th&gt;<br>
&lt;/tr&gt;<br>
&lt;tr&gt;<br>
&lt;td&gt;李强&lt;/td&gt;<br>
&lt;td&gt;张明&lt;/td&gt;<br>
&lt;td&gt;王平&lt;/td&gt;<br>
&lt;/tr&gt;<br>
&lt;/table&gt;</p>
<p>&lt;/center&gt;</p>
<h3>3.8 特殊字</h3>
<p>&lt;center&gt;</p>
<table>
<thead>
<tr>
<th style="text-align:center">特殊字符</th>
<th style="text-align:center">描述</th>
<th style="text-align:center">字符的代码</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center"></td>
<td style="text-align:center">空格符</td>
<td style="text-align:center"><code>&amp;nbsp;</code></td>
</tr>
<tr>
<td style="text-align:center">&lt;</td>
<td style="text-align:center">小于号</td>
<td style="text-align:center"><code>&amp;lt;</code></td>
</tr>
<tr>
<td style="text-align:center">&gt;</td>
<td style="text-align:center">大于号</td>
<td style="text-align:center"><code>&amp;gt;</code></td>
</tr>
<tr>
<td style="text-align:center">&amp;</td>
<td style="text-align:center">和号</td>
<td style="text-align:center"><code>&amp;amp;</code></td>
</tr>
<tr>
<td style="text-align:center">￥</td>
<td style="text-align:center">人民币</td>
<td style="text-align:center"><code>&amp;yen;</code></td>
</tr>
<tr>
<td style="text-align:center">©</td>
<td style="text-align:center">版权</td>
<td style="text-align:center"><code>&amp;copy;</code></td>
</tr>
<tr>
<td style="text-align:center">®</td>
<td style="text-align:center">注册商标</td>
<td style="text-align:center"><code>&amp;reg;</code></td>
</tr>
<tr>
<td style="text-align:center">°C</td>
<td style="text-align:center">摄氏度</td>
<td style="text-align:center"><code>&amp;deg;C</code></td>
</tr>
<tr>
<td style="text-align:center">±</td>
<td style="text-align:center">正负号</td>
<td style="text-align:center"><code>&amp;plusmn;</code></td>
</tr>
<tr>
<td style="text-align:center">×</td>
<td style="text-align:center">乘号</td>
<td style="text-align:center"><code>&amp;times;</code></td>
</tr>
<tr>
<td style="text-align:center">÷</td>
<td style="text-align:center">除号</td>
<td style="text-align:center"><code>&amp;divide;</code></td>
</tr>
<tr>
<td style="text-align:center">²</td>
<td style="text-align:center">平方（上标²）</td>
<td style="text-align:center"><code>&amp;sup2;</code></td>
</tr>
<tr>
<td style="text-align:center">³</td>
<td style="text-align:center">立方（上标³）</td>
<td style="text-align:center"><code>&amp;sup3;</code></td>
</tr>
</tbody>
</table>
<p>&lt;/center&gt;</p>
<p>版权归属 ©2019 择势勤</p>
<hr>