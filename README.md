# JavaScript console

---

> 原文：

使用console调试，前端开发是必不可少的。平时用的最多的是console.log(),但是console不止只有log这个方法。

# console是什么？

JS是没有console对象的，这是浏览器提供的对象。使用console对象可以在浏览器控制台输出信息，在不同的浏览器中输出效果可能不同。
火狐开发者文档对console的定义是：The Console object provides access to the browser's debugging console。

# 为什么用console不用alert？

alert弹出窗口会中断程序，如果alert是处于一个轮询中，只能在后台关闭浏览器进程，否则无法对浏览器进行任何操作。
alert显示字符串才有效，如果是显示对象只能看到[object]提示，因此用console好很多。

# 什么浏览器支持console。

支持console较好的浏览器是chrome和firefox，IE8以下的浏览器不支持，Safari支持。

# console都有些什么方法？

在chrome和IE11（后面都是用这两版本浏览器测试）下打印console对象。

[]()


# console的具体方法

## console.log()

console.log()用于在控制台输出日志信息，接受多个参数，参数之间用逗号分隔。

如果第一个参数使用格式占位符,console.log()方法将依次用后面的参数替换占位符，然后再进行输出。


占位符 类型
%s	字符串
%d,%i	整数
%f	浮点数
%o	对象超链接
%c	CSS格式化样式

console.info、console.debug和console.log的用法是一样的。

## console.assert()
assert方法，至少接收两个参数，第一参数是Boolean值。如果第一个参数是false，则输出一个错误信息，如果是true，什么也没输出。

## console.count()
在调用count()方法时记录次数，count()方法有个可选的参数。有个参数存在，则会输出该参数，后面跟着次数。

## console.dir()
显示指定的JavaScript对象的属性列表。

var object = {
	name: "Tom",
	age: "20"
}
console.dir(object);

var arr = [1,2,3,4];
console.dir(arr);

console.dir(document);

## console.dirxml(object)

把xml/html元素的xml/html 代码打印出来,等同于log.

## console.error()、console.warn()

error()控制台打印一段错误信息。warn()输出警告信息。

## console.group()、console.groupCollapsed()、console.groupEnd()

console.group()、console.groupCollapsed()和console.groupEnd()方法是显示分组信息，
唯一不同的是：console.group()默认信息展开，console.groupCollapsed()默认是折叠的。
console.groupEnd()表示分组结束。

console.group("第一组");
console.group("第二组");
console.log("日志输出");
console.log("日志输出");
console.groupEnd();
console.groupEnd();

console.groupCollapsed("第一组");
console.groupCollapsed("第二组");
console.log("日志输出");
console.log("日志输出");
console.groupEnd();
console.groupEnd();

## console.table()

console.table()方法是将对象用表格的方式显示。

var arr = [
	{name:"a"},
	{name:"b"},
	{name:"c"},
	{name:"d"}
];
console.table(arr);

## console.profile()和console.profileEnd()

这是分析一段代码的性能。可传入一个参数作为分析的名称。

function startProfile() {
	for(var i = 0; i < 255; i ++) {
		console.log(i);
		if(i == 200) {
			break;
		}
	}
}

console.profile("性能分析");
startProfile();
console.profileEnd();

# console.time()和console.timeEnd()

设置一个定时器记录一个操作需要花费的时间，可以传入一个参数作为定时器唯一的名称。

console.time("定时器");
for(var i = 0; i < 25; i ++) {
	console.log(i);
}
console.timeEnd("定时器");

# console.clear()
清空控制台。

# console.trace()
追踪函数的调用过程。

function functionA() {
	console.trace();	
}
function functionB() {
	console.log("b");
	functionA();
}

function functionC() {
	console.log("c");
	functionB();
}

function functionD() {
	console.log("d");
	functionC();
}
functionD();

# 值得注意的问题。

BSIE。IE浏览器如果不是在开发者调试模式下，调用console会报错。

可以通过以下方法解决：
1、
try {
	console.log("不在开发者模式下也可以调用console");
} catch(e){
	//这里将会报错，但我们不做任何事情
}

2、
if(window.console&&window.console.log) {
	console.log("这样调用console就不会报错啦");
}

参考文献：
https://developer.mozilla.org/en-US/docs/Web/API/Console
