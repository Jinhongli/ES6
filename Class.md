# Class

## CLass Declaration

使用`class`关键字声明一个类，其他的具体语法与一个对象字面量的声明类似。

```javascript
class PersonClass {
	// 构造函数
	constructor(name) {
		this.name = name;
	}

	// 原型上的公有方法
	sayName() {
		console.log(this.name);
	}
}

let person = new PersonClass('Nicholas');
person.sayName(); // "Nicholas"

console.log(person instanceof PersonClass); // true
console.log(person instanceof Object);      // true

console.log(typeof PersonClass);					// "function"
console.log(typeof PersonClass.prototype.sayName);  // "function"

```

对于`console.log(typeof PersonClass)`的结果为`function`，可以看出，`class`仅仅只是现有数据结构的语法糖(Syntactic Sugar)。

## Why Class

1. 不论是声明还是表达式，都不会提前(hosit)，所以存在TDZ。
2. 内部代码是严格模式，并且无法改变。
3. 所有的方法(公有)都是不可枚举的。
4. 所有的方法(公有)没有内部`[[Construct]]`方法，因此无法使用`new`方式调用。
5. 不使用`new`方式调用会报错。
6. 无法再次声明一个同名的`class`。但是可以在`class`声明之外重新赋值，但在`class`内部不行。

## First Class & IIFE

与`function`一样，`class`也可以作为参数传入。

```javascript
function createPerson(classPerson, name){
	return new classPerson(name);
}

let nicholas = createPerson(class {
	constructor(name){
		this.name = name;
	}
	sayName() {
		console.log(this.name);
	}
}, 'Nicholas');

console.log(nicholas.sayName()); // "Nicholas"
```

`class`的构造函数也可以立即调用，与IIFE类似。

```javascript

let nicholas = new class{
	constructor(name){
		this.name = name;
	}
	sayName(){
		console.log(this.name);
	}
}('Nicholas');

nicholas.sayName(); // "Nicholas"

```

## Accessor Properties

实例的自有属性在`constructor`中定义，而公有属性通过`get`和`set`来存取。

```javascript
class CustomHTMLElement {

    constructor(element) {
        this.element = element;
    }

    get html() {
        return this.element.innerHTML;
    }

    set html(value) {
        this.element.innerHTML = value;
    }
}

var descriptor = Object.getOwnPropertyDescriptor(CustomHTMLElement.prototype,
 "html");
console.log("get" in descriptor);   // true
console.log("set" in descriptor);   // true
console.log(descriptor.enumerable); // false

```

## Stactic Method

```javascript
class PersonClass {
    constructor(name) {
        this.name = name;
    }
    sayName() {
        console.log(this.name);
    }

    static create(name) {
        return new PersonClass(name);
    }
}

let person = PersonClass.create("Nicholas");
```

## Inheritance

使用`extends`实现类的继承

```javascript

class Rectangle {
	constructor(length, width){
		this.length = length;
		this.width = width;
	}
	getArea() {
		return this.length * this.width;
	}
}

class Square extends Rectangle {
	constructor(length){
		super(length, length);
	}
}

let square = new Square(3);

square.getArea(); // 9
console.log(square instanceof Square);      // true
console.log(square instanceof Rectangle);   // true

```

在子类中调用`super`方法来调用父类构造函数。

注意：

1. 只能在子类中使用`super`。
2. 在子类构造函数中，`super`必须在`this`之前调用。
3. 避免调用`super`的唯一方式就是在类的构造函数中`return`一个对象