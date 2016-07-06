---
title: "JavaScript编程精解"
date: 2016-06-25 21:35
tag: web
---

[TOC]

## JavaScript基础部分

数字(number): JavaScript 使用固定长度为64位的位序列来存储数字值。

几个特殊的数字：

* `Infinity`: 正无穷大
* `-Infinity`: 负无穷大
* `NaN`: 非数值，表示无意义的值

`typeof` 一元运算符，获取给定值的具体类型：

	typeof "abcd"
	"string"

布尔值：`true` / `false`

逻辑运算符：`&&` / `||` / `!`

未定义值 (两者基本等价)

* `null`
* `undefined`

JavaScript对于不同类型的运算或比较会进行自动类型转换。对于比较，可以使用严格比较：`===` 和 `!==`

`var`定义变量，可以同时定义多个变量，并用逗号分隔：

	var a = 1, b = 2;

几个函数：

* `alert`
* `confirm`
* `prompt`
* `isNaN`
* `Number` 强制转换为数值
* `console.log` 适合调试用

if语句：

	if (...)
	  ...;
	else if (...)
	  ...;
	else
	  ...;

while语句：

	while (...) {
	  ...;
	}

do..while语句：

	do {
	  ...;
	} while (...);  // 注意有分号

for循环：

	for (var i = 0; i <= 100; i++) {
	  if (i == 5)
	    break;  // break语句
	}

switch语句：

	switch (...) {
	  case condition1:
	    ...;
	    break
	  case condition2:
	    ...;
	    break
	  ...
	  default:
	    ...;
	    break
	}

对于switch, 每一个条件后加上`break`是个好习惯，否则比如匹配到condition1后，后面的语句都会执行，不管是否匹配的。如果没有任何匹配，则会跳到`default`标签。

注视：

* `//` 适合单行注释
* `/* .... */` 适合块注释

经验：

* 变量声明/定义都以`var`开头
* 语句都以`分号`结尾
* 缩进使用`2个空格`

函数定义的两种方式：

方式一，直接定义匿名函数，赋值给一个变量：

	var square = function(x) {
	  return x * x;
	};  // 分号结尾

	console.log(square(10));

方式二，直接做**函数声明**：

	console.log(square(10));
	
	function square(x) {
	  return x * x;
	}  // 无分号

这种方式不需要遵守从上而下的定义方式。

注：

* 注意函数中变量作用域，只有在函数内部用`var`定义的变量才属于函数内
* 在JS中，只有函数能够创建新的作用域
* JS对传入函数的参数数量几乎没有任何限制。如果有参数定义但是没有传参，则这些变量为undefined

当函数被调用时，函数体内部会添加一个特殊变量`arguments`，指向一个包含所有传入传输的对象。

此对象有length属性，和数组比较类似，但是不包含数组的任何方法

数组：

	> var arr = [1,2,3,4];
	> typeof arr
	'object'

数组也是一种对象

属性：如Math.max，mystr.length; 可以通过点号`.`或方括号`[]`获取，后者的key可以是带有空格的

	> ['a', 'b', 'c'].length
	3

方法：如mystr.toUpperCase()

	> typeof 'abc'.toUpperCase
	'function'
	> 'ABc'.toLowerCase()
	'abc'

数组的几个方法：

* join
* push: 在末尾添加
* pop: 在末尾删除
* unshift: 在开头添加
* shift: 在开头删除
* indexOf: 从第一个元素向后搜索
* lastIndexOf: 从最后一个元素向前搜索
* concat: 拼接两个数组(类似于python中的extend)
* slice: 取其中一部分数组 (不清楚这个和直接arr[i1:i2]有什么区别?)
对象：

创建对象的方式之一是使用大括号：

	var desc = {
	  work: 'program',
	  'my name': 'tanky',
	  'other': function() {
		return 'hello world';
	  }
	}

	> typeof desc
	'object'
	> desc.other();
	'hello world'

JS中对象的属性/方法是`**引用**`方式。

* `in` 二元操作符，判断属性或方法是否在对象中
* `delete` 一元操作符，从对象中移除指定的属性

可以直接通过`=`给对象的属性/方法赋值，如果属性/方法不存在，则相当于新增属性，否则相当于修改属性。

对于对象，引用两个相同的对象和两个不同对象包含相同属性是一样的：

	> var obj1 = {'value': 10};
	> var obj2 = obj1;
	> var obj3 = {'value': 10};
	> obj1 == obj2;
	true
	> obj1 == obj3;
	false
	> obj1.value = 15;
	15
	> obj2.value
	15
	> obj3.value
	10

遍历对象，使用`for (var name in object)`方式：

	> for (var i in desc) {
		console.log('k: ' + i + ', v: ' + desc[i]);
	  }
	k: work, v: program
	k: my name, v: tanky
	k: other, v: function () {
	return 'hello world';
	}

字符串、数字、布尔等都不是对象，所以不能添加属性，添加不会报错，不过没什么作用。

Math对象：

* min: 求最小值
* max: 求最大值
* sqrt: 求平方根
* 三角函数sin, cos, tan ...
* random: 0-1之间的随机数
* floor: 向下取整
* ceil: 向上取整
* round: 四舍五入

全局对象 `window`：每一个全局变量作为一个属性，存储在全局对象中。在浏览器中，全局对象存储在window变量中。

	> var a = 100;
	> 'a' in window;
	true

数组的`forEach`方法：

	function square_arr(arr) {
	  var n_arr = [];
	  arr.forEach(function(x) {
		n_arr.push(x * x);
	  });
	  return n_arr;
	}

	console.log(square_arr([1,2,3,4]));  // [1, 4, 9, 16]

数组的`filter`方法用于过滤：

	// 过滤出所有的奇数
	var arr = [1, 2, 3, 4, 5];

	console.log(arr.filter(function(v) {
	  return v % 2;
	}));

数组的`map`方法用于对每一个元素分别调用函数，生成一个新的数组：

	// 和上面forEach效果一样，对数组进行求平方
	var arr = [1, 2, 3, 4, 5];

	console.log(arr.map(function(v) {
	  return v * v;
	}));

数组的`reduce`方法用于折叠数组，接收用于合并操作的函数以及初始值，如果初始值没写，则默认表示0；合并函数接收两个参数，即前一次和本次：

	// 数组所有元素求和
	var arr = [1, 2, 3, 4, 5];

	console.log(arr.reduce(function(pre, cur) {
	  return pre + cur;
	}));

函数的`apply`方法，接收一个数组或类数组的参数（所以可以把arguments传过去）

函数的`call`方法，接收一系列参数，和`apply`相比相当于把参数数组展开

函数的`bind`方法新生成一个函数，并把传递的参数当做上下文一起传过去。

参考：

* [What is the difference between call and apply?](http://stackoverflow.com/questions/1986896/what-is-the-difference-between-call-and-apply)
* [Javascript call() & apply() vs bind()?](http://stackoverflow.com/questions/15455009/javascript-call-apply-vs-bind)


与JSON相关的两个方法：

* `JSON.stringify`：输入javascript变量，返回JSON编码后的字符串
* `JSON.parse`：输入一个字符串，返回解码后的值

在调用object.method()时，对象中的一个特殊变量`this`会指向当前方法所属的对象。

原型(prototype)：原型是另一个对象，是对象的属性来源，当访问一个对象不包含的属性时，会从对象原型中搜索属性，接着是原型的原型...

JS对象原型的关系是一种树形结构，根部就是Object.prototype；

子对象可以继承父对象的属性。

原型是一层层继承下来，比如函数继承自原型Function.prototype，数组继承自Array.prototype。

通过`Object.getPrototypeOf()`返回一个对象的原型：

	function func() {
	};

	// true
	console.log(Object.getPrototypeOf(func) == Function.prototype);

通过`Object.create`利用一个特定的原型来创建对象。

	var protoObj = {
	  say: function() {
		console.log('hello');
	  }
	};

	var my_obj = Object.create(protoObj);
	// print 'hello'
	my_obj.say();

	// true
	console.log(Object.getPrototypeOf(my_obj) == protoObj);

构造函数：

(**这块内容有点绕，需额外再研究下**)

在JS中，调用函数之前添加一个关键字`new`则表示调用其构造函数；构造函数中包含了指向新对象的变量this。

通过关键字`new`创建的对象称之为构造函数的实例。

构造函数的名称一般以大写字母开头，便于与其它函数区分。

所有使用特定构造函数创建的对象，都会将构造函数的prototype属性作为其原型。

	function Rabbit(type) {
	  this.type = type;
	}

	var killerRabbit = new Rabbit("killer");
	var blackRabbit = new Rabbit("black");
	// black
	console.log(blackRabbit.type);

	Rabbit.prototype.speak = function(line) {
	  console.log("The " + this.type + " rabbit says '" + line + "'");
	};

	blackRabbit.speak("Hello...");

关于原型，有`可枚举(enumerable)`和`不可枚举(nonenumerable)`属性：

* 可枚举：我们创建并赋予对象的所有属性
* 不可枚举：Object.prototype中的标准属性

`in` 可以测试属性是否在对象中：

	var map = {'one': 1, 'two': 2}

	Object.prototype.nonsense = "hi";

	// one
	// two
	// nonsense  <-- nonsense也在
	for (var n in map)
	  console.log(n);

	// true
	console.log("nonsense" in map);
	// true
	console.log("toString" in map);

`Object.defineProperty`函数可以定义自己的不可枚举属性：

	var map = {'one': 1, 'two': 2}

	Object.defineProperty(Object.prototype, "hiddenNonsense",
						  {enumerable: false, value: "hi"});

	// one
	// two
	for (var n in map)
	  console.log(n);

	// true
	console.log("hiddenNonsense" in map);
	// "hi"
	console.log(map.hiddenNonsense);

`in`并不能判断属性是自身还是原型中继承的，可以通过`hasOwnProperty`方法来判断：

	// false
	console.log(map.hasOwnProperty('toString'));

`instanceof`二元运算符用于判断某个对象是否继承自指定的构造函数：

	function Func1(text) {
	  this.text = text;
	}

	function Func2 (text) {
	  Func1.call(this, text);
	}
	Func2.prototype = Object.create(Func1.prototype);  // 继承

	console.log(new Func2('a') instanceof Func2);  // true
	console.log(new Func2('a') instanceof Func1); // true
	console.log(new Func1('a') instanceof Func2); // false

调试相关：

启用严格模式：在文件或函数体顶部加上字符串`"use strict"`

	function func() {
	  "use strict"
	  ...
	}

> 我们必须遏制住随意修改代码进行调试的冲动，思考才是最重要的。

1. 有目的的在程序中使用console.log输出额外信息
2. 断点：浏览器一般可以直接设置断点，或者使用`debugger`语句

(chrome下打开开发者工具->Sources, 找到相应JS代码，点击行号增加断点, 具体可以参考[chrome js debugging](https://developer.chrome.com/devtools/docs/javascript-debugging))

异常：`try .. catch .. finally`，其中finally可选，catch 到的异常值会绑定到圆括号中的变量：

	function func(value) {
	  if (value == 5)
		throw new Error("value can't equel 5");
	}

	try {
	  func(5);
	} catch (error) {
	  console.log('error: ', error);
	} finally {
	  console.log('exit with clean task...');
	}

JS并未对选择性捕获异常提供良好的支持，要不捕获所有异常，要不什么都不捕获。只能靠额外来支持：

	function InputError(msg) {
	  this.message = msg;
	  this.stack = (new Error()).stack;
	}
	InputError.prototype = Object.create(Error.prototype);
	InputError.prototype.name = 'InputError';

	function func(value) {
	  if (value == 5)
		throw new InputError("value can't equel 5");
	}

	try {
	  func(5);
	} catch (error) {
	  // if (! (error instanceof InputError))
	  if (error instanceof InputError)
		console.log('input error: ', error);
	} finally {
	  console.log('exit with clean task...');
	}

最后就是实现断言这个工具函数了，JS自身是没有提供这个语句：

	function AssertionFailed(message) {
	  this.message = message;
	}
	AssertionFailed.prototype = Object.create(Error.prototype);

	function assert(test, message) {
	  if (!test)
		throw new AssertionFailed(message);
	}


## TODO

* 未定义值null和undefined不等价的情况?
* 函数 - 闭包
* 创建对象的另外一种方式?
* JS 正则
* 第十章 模块