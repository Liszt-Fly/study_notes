---
tags:JavaScript,Houdunren
---

1. [1 变量](#1-变量)
2. [2 体验解析过程和变量提升](#2-体验解析过程和变量提升)
3. [3 let const var](#3-let-const-var) 1. [块级作用域](#块级作用域)
   1. [let var const 的差异](#let-var-const-的差异)
      1. [var](#var)
      2. [let](#let)
      3. [const](#const)

# 1 变量

JavaScript 是弱类型动态语言，主要可以体现在以下几个方面：

1.不具有各种静态类型，均使用 var,let,const 进行声明

```javascript
var web = "houdunren" //string
var age = 10 //number
var test = {} //object
```

2.在声明变量之后仍然可以修改变量的类型和值类型

```javascript
var web = "https://houdunren.com"
console.log(typeof web) //string
web = 30
console.log(typeof web) //number
web = {}
console.log(typeof web) //object
```

# 2 体验解析过程和变量提升

代码文件

```javascript
console.log(web)
var web = "https://houdunren.com"
```

实际解析编译过程

```javascript
var web
console.log(web) //运行到这一行代码的时候输出undefined
web = "https://houdunren"
```

> **变量提升**:在使用 var 声明变量的时候，解析过程总会将变量声明提前到代码块的最前面

赋值过程不会进行提升，仍然处于原来的位置,JavaScript 是单线程语言，所以执行肯定是按顺序执行。但是并不是逐行的分析和执行，而是一段一段地分析执行，会先进行编译阶段然后才是执行阶段。

# 3 let const var

### 块级作用域

- { } 由大括号构成的块级作用域

- function(){} 由函数体构成的块级作用域
- module 文件 由模块构成的块级作用域，一个 module 代表一个块级作用域

- for 循环 一个循环体是一个作用域

```javascript
//作用域1
{
	var a = 1
}
//作用域2
function hd() {
	var b = 1
}
//作用域3
;<script type="text/javascript" src="./1.js"></script>
//作用域4
for (var i = 0; i < 10; i++) {}
```

> 特别注意：除 function 函数作用域之外，对于 var 声明的变量，均不受块作用域的影响

## let var const 的差异

### var

var 是 javascript 早期的产物，现在不建议使用 var 进行变量声明，但是需要一定的了解

- var 可以重复进行声明

```javascript
var a = 1
var a = "hello"
```

- var 不具有除了函数体之外的块级作用域

```javascript
{
	var a = 1
}
console.log(a) //1 可以正常穿透，不受影响
```

循环体是特别经典的例子

```javascript
var i = 99
for (var i = 0; i < 5; i++) {
	//var 没有块作用域
	console.log(i)
}

console.log(i) //5
```

- 变量提升特性
- var 声明的变量都押入了 windows 对象中存储

### let

let 是 var 更完美的版本，在声明变量的时候，更建议使用 let 而不是 var

- let 必须先声明后使用，否则会形成暂时性死区 TDC

```javascript
console.log(web)
let web = "houdunren" //Can not access "web" before initialization
```

- let 拥有更健壮的块级作用域

```javascript
let m = 99
for (let m = 0; m < 5; m++) {
	console.log(m)
}
console.log(m) //99 可以看出并没有受到循环的影响
```

```javascript
{
	let age = 10
}
console.log(age) //不属于同一个作用域，无法访问
```

- let 不可以重复进行声明
- let 声明的变量不会押入 window 对象中

### const

const 具有 let 所有的特性，但是 const 声明的变量不可变
对于不可变性，需要进行分类讨论：
const 修饰值类型

```javascript
const a = 1
a = 2 //error
```

const 修饰引用类型

```javascript
const b = { age: 5 }
b.age = 10
console.log(b.age) //10
```

> 对于值类型，const 指值为常量，如果值改变
