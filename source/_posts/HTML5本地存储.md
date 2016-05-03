title: HTML5本地存储
date: 2016-04-22 13:30:42
tags: [h5本地存储]
categories: [HTML5]
---

## localStorage和sessionStorage

### 定义

* `localStorage` 是*没有时间限制*的数据存储，也就是说永远不会过期，除非主动删除数据。数据可以跨越多个窗口，同一域名下所有页面共享数据。
* `sessionStorage` 是针对一个session的数据存储，按窗口区分，同一窗口下，一个网站的任何页面都可以共享数据。每个窗口的数据都是独立的，它的数据会因窗口的关闭而丢失，不同窗口直接的`sessionStorage`不可以共享。
* 对比cookie:本地存储空间更大（5M左右，cookie约5kb，一般用来存用户登录信息），操作方便，ie8+都可以支持。

### API

`localStorage`和`sessionStorage`有相同的API，如：

* `localStorage.length`	获取存储数据的个数
* `localStorage.key(n)`	获取第n条数据的键值
* `localStorage.key_old = key_new`	修改第n条数据的键
* `localStorage.setItem(key, value)`	添加某条数据
* `localStorage.getItem(key)`	获取某条数据
* `localStorage.removeItem(key)`	移除某条数据
* `localStorage.clear`	清除所有数据

也可以用对象的方法添加获取数据，如：

* `localStorage.name="liuwei";`	添加数据
* `console.log(localStorage.name);`	获取数据

### 通过StorageEvent事件响应存储变化

无论何时，`Storage`对象发生变化时（即创建、更新、删除数据项时，重复设置相同的键不会触发该事件，`Storage.clear()`至多触发一次该事件），`StorageEvent`事件会触发。在同一个页面内发生的改变不会起作用——在相同域名下的其他页面（如一个新标签或iframe），发生的改变才会起作用。其他域名下的页面不能访问相同的Storage对象。使用方法，如：

	window.addEventListener('storage', function(e) {
		document.querySelector('.my-key').innerHTML = e.key;
		document.querySelector('.my-old').innerHTML = e.oldVale;
		document.querySelector('.my-new').innerHTML = e.newValue;
		document.querySelector('.my-url').innerHTML = e.url;
		document.querySelector('.my-storage').innerHTML = e.storageArea;
	});

这里，我们为window对象添加了一个事件监听器，在当前域名相关的`Storage`对象发生改变时被触发。此事件相关的事件对象有多个属性包含了有用的信息——改变数据项的键，改变前的值，改变后的值，改变的存储对象所在的文档URL，以及存储对象本身。

### 可能的实际应用

* 页面刷新之后需要维持改变后的状态，如页面的一些改变后的样式，关闭开启的菜单项等等；
* 跨页面跟踪状态，如a页面做了修改，在b页面显示出这些修改；

### 实例参考

* [MDN Web Storage介绍](https://developer.mozilla.org/zh-CN/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API "MDN Web Storage介绍")
* [开启关闭菜单项实例](http://www.zhangxinxu.com/wordpress/2011/09/html5-localstorage%E6%9C%AC%E5%9C%B0%E5%AD%98%E5%82%A8%E5%AE%9E%E9%99%85%E5%BA%94%E7%94%A8%E4%B8%BE%E4%BE%8B/ "开启关闭菜单项实例")
