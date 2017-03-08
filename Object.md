# Obejct

## Object Literal

ES6简化了对象字面量的语法，具体用法为：

- 键值相同。JS引擎在遇到这种情况时，会在当前作用域搜索同名变量`name`，然后将该变量的值付给对象字面量的`name`属性。

```javascript

// ES5
function createPerson(name, age){
	return {
		name: name,
		age: age
	}
}

// ES6
function createPerson(name, age){
	return {
		name,
		age
	}
}

```

- 方法简写。省略了`:`与`function`关键字。

```javascript

// ES5
var person = {
    name: 'Nicholas',
    sayName: function() {
        console.log(this.name);
    }
};

// ES6
var person = {
	name: 'Nicholas',
	sayName() {
		console.log(this.name);
	}
}

```

- 属性名可计算。

```javascript
var lastName = 'last name';

var person = {
    'first name': 'Nicholas',
    [lastName]: 'Zakas'
};

console.log(person['']);      // 'Nicholas'
console.log(person[lastName]);          // 'Zakas'
```

## New Methods

- `Object.is()`

传入两个参数进行对比，返回布尔值。与`===`类似，但是修复了一些看起来奇怪的情况：

```javascript
console.log(+0 == -0);              // true
console.log(+0 === -0);             // true
console.log(Object.is(+0, -0));     // false

console.log(NaN == NaN);            // false
console.log(NaN === NaN);           // false
console.log(Object.is(NaN, NaN));   // true

console.log(5 == 5);                // true
console.log(5 == '5');              // true
console.log(5 === 5);               // true
console.log(5 === '5');             // false
console.log(Object.is(5, 5));       // true
console.log(Object.is(5, '5'));     // false
```

- `Object.assing()`

传入两个对象，将第二个参数对象的属性及方法复制(添加或覆盖)给第一个对象。

```javascript
var source = {
	a: function(){},
	b: 'b',
	c: [1,2,3]
};

var target = {};

Object.assign(target, source);
console.log(target);
```
