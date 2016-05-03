title: CSS3选择器
date: { { date } }
categories: CSS
tags: [CSS3选择器]
---

## CSS3选择器

### 1.属性选择器

`ele[att=val]{}` 	#选择属性等于val的元素
`ele[att*=val]{}`	#选择属性包含val的元素
`ele[att^=val]{}` 	#选择属性以val开头的元素
`ele[att$=val]{}` 	#选择属性以val结束的元素

### 2.伪元素选择器和结构性伪类选择器

`p:first-line{}` #选择p标签第一行
`p:first-letter{}` #选择p标签第一个字
`p:before{content:'a'}` #p标签之前插入内容a
`p:after{content:url(test.wav)}` #p标签之后插入内容test.wav

`:root{background:#ccc}` :root选择器 设置整个html
`body \*:not(h1){}` :not选择器 设置body下所有元素，除了h1
`:empty{}` :empty选择器 设置内容为空的所有元素
`:target{}` :target选择器 设置锚点指定位置

### 3.子元素选择器

`li:first-child{}` #第1个li
`li:last-child{}` #最后1个li
`li:nth-child(2){}` #第2个li
`li:nth-last-child(2){}` #倒数第2个li
`li:nth-child(odd){}` #li父元素下第奇数个元素是li的元素（有时候会出错）
`li:nth-child(even){}` #li父元素下第偶数个元素是li的元素
`li:nth-of-type(odd){}` #li父元素下第奇数个li元素（同元素相比）
`li:nth-of-type(even){}` #li父元素下第偶数个li元素（同元素相比）
`li:nth-last-of-type(n){}` #同上
`li:only-child{}` #只有一个li元素的元素列表
`ele::selection{}` #选中ele时的样式

### 4.通用兄弟元素选择器

`div ~ p` #div兄弟元素p