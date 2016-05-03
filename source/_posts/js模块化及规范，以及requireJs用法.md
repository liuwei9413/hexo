title: js模块化及规范，以及requireJs用法
date: 2016-02-22 11:30:11
tags: [js模块化]
---

## js模块化原理

### 定义

模块就是实现特定功能的一组方法

### 基本写法
	
	//自执行匿名函数包裹模块
	var module1 = (function($) {
		//$...
		var fn1 = function() {
			//方法fn1...
			console.log(1)
		};
		var fn2 = function() {
			//模块fn2...
		};
		
		//对外接口
		return {
			fn1 : fn1,
			fn2 : fn2
		}
	})(jQuery);	//保持模块的独立性，将全局变量传入模块内部
	
	//模块继承
	var module2 = (function(mod) {
		mod.fn3 = function() {
			//方法fn3...
			console.log(3);
		};			
		
		return mod;
	})(window.module1 || {});

	module2.fn1(); //1
	module2.fn3(); //3

## AMD及CMD规范

### AMD规范（单线程异步加载模块）
	
	//异步加载test.js，浏览器不会假死，当test.js加载完成，执行后面的回调函数
	require(['test'], function(test) {
		test.doSomething();
	})

### CMD规范（多线程同步加载）

	//同步加载test.js，浏览器可能会假死
	var test = require('test');
	test.doSomething();

## requireJs用法

### 引入requireJS文件，确认主模块
	<!--防止加载requireJs文件时浏览器出现假死：1.请求放到最底部；2.异步加载-->
	<script src="js/require.js" defer async="true" data-main="js/main.js"></script>

### 主模块写法

require()函数接受两个参数，第一个参数为数组，表示主模块所依赖的模块，第二个参数是一个回调函数，当数组内指定的模块都加载成功时调用，并将加载的模块以参数形式传入回调函数，从而在回调函数内可以使用这些模块。

	require(['module1', 'module2', 'module3'], function(module1, module2, module3) {
		//...
	})

	//main.js 依赖a.js,b.js,jquery
	require.config({
		paths : {
			'jquery' : 'http://apps.bdimg.com/libs/jquery/2.1.4/jquery.min',
			'b' : 'lib/b'
		}
	});
	
	require(['jquery', 'a', 'b'], function($, A, B) {
		$('body').css('background', '#ccc');	//依赖jq
		console.log(A.add(1, 1));	//2
		console.log(B.result());	//6
	});
	
	

paths属性指定各个模块路径

	require.config({
		paths : {
			'jquery' : 'http://apps.bdimg.com/libs/jquery/2.1.4/jquery.min',
			'b' : 'lib/b'	//指定b.js路径为mian.js同一目录文件夹lib下的b.js
		}
	});

### AMD模块的写法

require.js加载的模块采用AMD规范，模块必须采用特定的define()函数定义。

1.不依赖其他模块
	
	//a.js
	define(function() {
		var add = function(a, b) {
			return a + b;
		};
	
		return {
			add : add
		}
	});

2.b模块依赖a模块
	
	//b.js
	define(['a'], function(A) {
		function result() {
			return A.add(3, 3);
		};
	
		return {
			result : result
		}
	})

### 注意事项：

1.模块路径均以主模块main.js为参考，相对路径如a.js，可以直接用a（.js后缀默认添加）；
2.require.config({}); 修改默认配置，放在main.js头部；