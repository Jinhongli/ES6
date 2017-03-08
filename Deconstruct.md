# Deconstruct

## Object Deconstruct

```javascript
let node = {
        type: "Identifier",
        name: "foo"
    };

let { type, name } = node;

console.log(type);      // "Identifier"
console.log(name);      // "foo"
```

需要注意的是：

1. 必须初始化或赋值。
2. 右侧表达式不能为`null`或`undefined`。
3. 默认值为`undefind`。也可以使用`flag = true;`的方式指定默认值。

## Array Deconstruct

```javascript
let colors = [ "red", "green", "blue" ];

let [ firstColor, secondColor ] = colors;
let [ , , thirdColor ] = colors;

console.log(firstColor);        // "red"
console.log(secondColor);       // "green"
console.log(thirdColor);       // "blue"
```

### 用于变量交换

```javascript
var a = 1,
	b = 2;
[a, b] = [b, a];
```

### 用于函数参数

```javascript
function setCookie(name, value, { secure, path, domain, expires } = {}) {

    // ...
}
```