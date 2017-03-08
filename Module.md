# Module

## Basic Export

使用`export`关键字来导出模块内容。

```javascript
export var color = "red";
export let name = "Nicholas";
export const magicNumber = 7;

export function sum(num1, num2) {
    return num1 + num1;
}

export class Rectangle {
    constructor(length, width) {
        this.length = length;
        this.width = width;
    }
}

function subtract(num1, num2) {
    return num1 - num2;
}

function multiply(num1, num2) {
    return num1 * num2;
}

export { multiply };
```

需要注意的是：

1. `function`和`class`需要具有`name`属性。
2. 不仅可以导出(`export`)一个声明，还可以导出一个引用，如`multiply`，导出了一个对象，具有`multiply`函数的应用。[此处的只有`key`是ES6中`Object`的简写方式]
3. 可以不到处一个属性或方法，如`subtract`，这就是模块的私有方法。

## Basic Import

使用`import`关键字来引入一个模块。

```javascript
import { sum } from "./example.js";
import { sum, multiply, magicNumber } from "./example.js";
import * as example from "./example.js"; // 导入所有
```

`from`关键字指明模块的位置。

需要注意的是：

1. 导入的变量，相当于使用`const`声明。
2. 这里的语法看似对象结构，但并不是。

## Default Values

导出模块的默认值，可以在`export`后面添加`default`关键字。

```javascript
function sum(num1, num2) {
    return num1 + num2;
}

export default sum;
```

这样的话，导入模块时就只需要指定模块名就可以了。

```javascript
import sum from "./example.js";

console.log(sum(1, 2));     // 3
```