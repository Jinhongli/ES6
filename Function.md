# Function

## Default Parameter

对于函数中参数的默认值，ES5一般通过`||`短路逻辑来实现，严谨一些通过判定`undefined`，如下：

```javascript
function ajax(url, timeout, callback){

	timeout = timeout || 2000;
	callback = (typeof callback !== 'undefined') ? callback : function(){...};

	...

}
```
在ES6中可以使用默认参数：

```javascript
function ajax(url, timeout=2000, callback=function(){...}){

	...

}
```

需要注意的是：

1. 默认参数判定`undefined`，因此`null`被认为是有效值。
2. 非严格模式中，改变默认参数，`arguments`会发生改变；而严格模式中则不会改变。

## Rest Parameter

对于函数中的未命名参数，ES5中使用`arguments`变量来调用。

```javascript
function pick(book){
	let result = Obejct.create(null);

	for(let i=1, len=arguments.length;i<len;i++){
		result[arguments[i]] = book[arguments[i]];
	}

	return result;
}

let book = {
	title: 'Understanding ECMAScript 6',
	author: 'Nicholas C. Zakas',
	year: 2015
};

let bookData = pick(book, 'author', 'year');

console.log(bookData.author); // Nicholas C. Zakas
console.log(bookData.year); // 2015
```

但是这种方式的缺点：

1. 没有显示表明函数具有未命名参数。
2. 未命名参数在`arguments`的参数顺序不一致。

在ES6中，通过**剩余参数**(rest parameter)来处理，剩余参数使用`...rest_para`来表示，其中`rest_para`是剩余参数的变量名，是一个包含着传入函数的剩余实参的`Array`。那么上面的`pick()`就可以改写为：

```javascript
function pick(book, ...rest){
	let result = Obejct.create(null);

	for(let i=0, len=rest.length;i<len;i++){
		result[rest[i]] = book[rest[i]];
	}

	return result;
}
```

使用中需要注意的是：

1. 剩余参数并不会影响函数的`length`属性。
2. 剩余参数之后不能再出现具名参数。
3. 剩余参数不能用于对象的`setter`函数中。

## Spread Operator

扩展运算符与剩余参数用法近似，均使用`...`，但产生的效果相反。

**剩余参数**是将独立的参数合并为数组，而**扩展运算符**则是将数组展开为独立的参数。

```javascript
let values = [1,2,5,4,3];

// ES5
console.log(Math.max.apply(Math, values)); // 5

// ES6
console.log(Math.max(...values)); // 5

// 与其参数一同使用 
console.log(Math.max(6, ...values, 7)); // 7
```

通俗一些就是：

**扩展运算符**在调用函数时使用，将数组转换成独立的参数传入

**剩余参数**在声明函数时使用，将传入的独立参数转换成数组来使用


## Arrow Function

箭头函数用`=>`来定义，与传统函数相比：

1. 没有`this`, `super`, `arguments`, `new.target`绑定。而函数内部的`this`等变量的值均为父级非箭头函数的相应变量。
2. 不能使用`new`方式调用，否则会报错。
3. 没有原型。
4. 函数内部无法改变`this`。
5. 参数不能重复

箭头函数具体语法：

```javascript
// 一个参数
var reflect = value => value;

var reflect = function(value){
	return value;
}

// 两个参数
var sum = (num1, num2) => num1+num2;

var sum = function(num1, num2){
	return num1+num2;
}

// 没有参数
var getName = () => 'Nicholas';

var getName = function(){
	return 'Nicholas';
}

// 函数体有多个语句
var add = (num1, num2) => {
	var sum	= num1 + num2;
	return sum;
}

// 空函数
var empty = () => {};
var empty = function(){};
```

常见用途：

1. 立即执行函数IIFE
2. 事件绑定this
3. 传入函数