title: Markdown 学习笔记
date: 2015-12-04 11:20:49
tags: [Markdown]
categories: [editor]
---

## Markdown 学习笔记

### 段落和换行
一个 Markdown 段落是由一个或多个连续的文本行组成，它的前后要**有一个以上的空行**（空行的定义是显示上看起来像是空的，便会被视为空行。比方说，若某一行只包含空格和制表符，则该行也会被视为空行）。普通段落不该用空格或制表符来缩进。

### 标题
Markdown支持两种标题的语法，**Setext**  和 **atx** 形式。利用 `= `（最高阶标题）和 `-` （第二阶标题），Atx 形式在行首插入 1 到 6 个 `#` ，对应到标题 1 到 6 阶。

    This is an H1
    =============

	This is an H2
	-------------
类 Atx 形式则是在行首插入 1 到 6 个 # ，对应到标题 1 到 6 阶，例如：

    # 这是 H1
	## 这是 H2
	###### 这是 H6

### 区块引用 Blockquotes
Markdown 标记区块引用是使用类似 email 中用 `>` 的引用方式。如果你还熟悉在 email 信件中的引言部分，你就知道怎么在 Markdown 文件中建立一个区块引用，那会看起来像是你自己先断好行，然后在每行的最前面加上 `>` ：
区块引用可以嵌套（例如：引用内的引用），只要根据层次加上不同数量的 > ：

    > This is the first level of quoting.
	>
	> > This is nested blockquote.
	>
	> Back to the first level.

### 列表
Markdown 支持有序列表和无序列表。
无序列表使用星号、加号或是减号作为列表标记：

	*   Red
	*   Green
	*   Blue

有序列表则使用数字接着一个英文句点：

	1.  Bird
	2.  McHale
	3.  Parish

### 代码区块
要在 Markdown 中建立代码区块很简单，只要简单地缩进 4 个空格或是 1 个制表符就可以，例如，下面的输入：

这是一个普通段落：

    这是一个代码区块。

Markdown 会转换成：

	<p>这是一个普通段落：</p>

	<pre><code>这是一个代码区块。
	</code></pre>

### 分割线

你可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格。下面每种写法都可以建立分隔线：

	* * *
	
	***
	
	*****
	
	- - -
	
	---------------------------------------

***

### 链接

Markdown 支持两种形式的链接语法： 行内式和参考式两种形式。

不管是哪一种，链接文字都是用 [方括号] 来标记。

要建立一个行内式的链接，只要在方块括号后面紧接着圆括号并插入网址链接即可，如果你还想要加上链接的 title 文字，只要在网址后面，用双引号把 title 文字包起来即可，例如：

	This is [an example](http://example.com/ "Title") inline link.

	[This link](http://example.net/) has no title attribute.

会产生：

	<p>This is <a href="http://example.com/" title="Title">
	an example</a> inline link.</p>
	
	<p><a href="http://example.net/">This link</a> has no
	title attribute.</p>

如果你是要链接到同样主机的资源，你可以使用相对路径：

	See my [About](/about/) page for details.

参考式的链接是在链接文字的括号后面再接上另一个方括号，而在第二个方括号里面要填入用以辨识链接的标记：

	This is [an example][id] reference-style link.

接着，在文件的任意处，你可以把这个标记的链接内容定义出来：

	[id]: http://example.com/  "我是title"
	
链接内容定义的形式为：

+ 方括号（前面可以选择性地加上至多三个空格来缩进），里面输入链接文字
+ 接着一个冒号
+ 接着一个以上的空格或制表符
+ 接着链接的网址
+ 选择性地接着 title 内容，可以用单引号、双引号或是括弧包着(测试单引号有问题)

下面这三种链接的定义都是相同：

	[foo]: http://example.com/  "我是title"
	[foo]: http://example.com/  '我是title'
	[foo]: http://example.com/  (我是title)
	
你也可以把 title 属性放到下一行，也可以加一些缩进，若网址太长的话，这样会比较好看：

	[id]: http://example.com/longish/path/to/resource/here
	    "我是title"

链接辨别标签可以有字母、数字、空白和标点符号，但是并不区分大小写，因此下面两个链接是一样的：

	[link text][a]
	[link text][A]

隐藏链接标记功能让你可以省略指定链接标记，这种情况下，链接标记会视为等同于链接文字，用隐藏链接标记只要在链接文字后加上一个空的方括号，例如“baidu.com” 链接到 baidu.com ,可以简化成：

	[baidu][]

然后定义链接内容：

	[baidu]: http://www.baidu.com/ "百度一下，你就知道"

[baidu][]
[baidu]: http://www.baidu.com/ "百度一下，你就知道"

下面是是一个参考式链接的范例：

	I get 10 times more traffic from [Google] [1] than from
	[Yahoo] [2] or [MSN] [3].
	
	  [1]: http://google.com/        "Google"
	  [2]: http://search.yahoo.com/  "Yahoo Search"
	  [3]: http://search.msn.com/    "MSN Search"

### 强调

使用 `*` 和 `_` 作为标记强调字词的符号，被 `*` 和 `_` 包围的字词会被转成 `<em>` 和 `<strong>` ，例如：

    *我会被转为<em>标签包围*

	**我会被转为<strong>标签包围**

### 代码

如果要标记一小段行内代码，可以用反引号 ` 包含起来，例如：

`<script>`

### 图片

Markdown 使用一种和链接相似的语法来标记图片，允许两种样式：**行内式** 和 **参考式**

**行内式：**

	![alt 图片alt描述](/path/to/img.jpg)
	
	![alt 图片alt描述](/path/to/img.jpg "图片title")

详细叙述如下：

+ 一个惊叹号 !
+ 接着一个方括号，里面放上图片的替代文字
+ 接着一个普通括号，里面放上图片的网址，最后还可以用引号包住并加上 选择性的 'title' 文字。

**参考式：**

	![alt 图片描述][id]
	
	[id]: /path/to/img.jpg "图片title"

### 反斜杠

Markdown 可以利用反斜杠来插入一些在语法中有其它意义的符号，例如：如果你想要用星号加在文字旁边的方式来做出强调效果（但不用 <em> 标签），你可以在星号的前面加上反斜杠：	

	\*我不要转成<em>\*

Markdown 支持以下这些符号前面加上反斜杠来帮助插入普通的符号：

	\   反斜线
	`   反引号
	*   星号
	_   底线
	{}  花括号
	[]  方括号
	()  括弧
	#   井字号
	+   加号
	-   减号
	.   英文句点
	!   惊叹号

### 总结

以上就是 `Markdown`的语法，感谢巨人的肩膀！！！