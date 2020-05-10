# 函数

### 函数声明

```js
// function statements -- 有名函数

function fn() {
	console.log(1)
}
fn() // 1

// 函数声明 -- 匿名函数,不进行赋值会报错
function () {} // SyntaxError: Function statements require a function name
```

---

### 函数表达式

```js
// function expression

var fn = function() {
	console.log(1)
}
fn() // 1
```

!> 函数表达式可以直接跟**`()`**自执行，函数声明必须通过**`fn()`**来调用

```js
// 函数表达式 -- 跟括号自执行

var fn = function() {
	console.log(1)
}() // 1

// 函数声明 -- 跟括号会报错
function fn() {
	console.log(1)
}() // SyntaxError: Unexpected token ')'
```

---

### 形参/实参

```js
function fn(a, b){ // a, b 为形参
	console.log(a + b)
}
fn(1, 2) // 1，2 为实参
```

---

### 默认返回值

​		函数执行结束，默认返回**`undefined`**

```js
// 函数默认返回值
function fn(a, b) {
	var result = a + b
}
var num = fn(1, 2) // undefined -- 函数执行结束，默认返回undefined
```

---

### return

​		**`return`**  ---  通过**`return`**能够修改函数的默认返回值，一个函数里边只能有一个return，遇到return函数立即停止运行，并且将**`return`**后面的值作为结果返回出来。

```js
// 修改函数的默认返回值
function fn(a, b) {
	return a + b
}
var num = fn(1, 2) // 3

// 简单封装通过id获取元素的方法
function getId(string) {
	return document.getElementById(string)
}
var box = document.getId('box') // 获取id名为box的元素
```

---

### this

!>  `this是在函数调用时发生的绑定，它指向什么完全取决于函数是在哪里被调用，而不是取决于函数是在哪里被定义`。

#### 全局环境

​		全局环境的**`this`**指向顶层对象

```js
// 浏览器
console.log(this) // window

// node
console.log(this) // globe
```

---

#### 函数自执行

​		函数不依赖任何环境被直接调用时，非严格模式下**`this`**指向顶层对象，严格模式下**`this`**指向 undefined，这样做是为了消除 JavaScript 中一些不严谨的行为。

```js
// 非严格模式
function fn() {
	console.log(this)
}
fn() // window

// 严格模式
'use strict'
function fn() {
	console.log(this)
}
fn() // undefined

// 为了避免全局污染，可以将以上代码放入一个自执行函数中
;(function () {
	'use strict'
	console.log(this) // undefined
})()
```

---

#### 作为对象方法调用

​		当函数作为对象的方法被调用时，**`this`**指向当前这个对象

```js
function fn() {
	console.log(this)
}

var obj = {
	a: fn
}

obj.a() // {a: f}
document.onclick = fn // #document
box.onclick = fn // <div id="box"></div>
```

---

### arguments

​		当不确定形参个数时，就可以使用**`不定参`**，不定参为一个**`伪/类数组对象`**，有**`length`**属性

```js
function fn() {
	console.log(arguments) // Arguments(4) [1, 2, 3, 4, callee: ƒ, Symbol(Symbol.iterator): ƒ]
}
fn(1, 2, 3, 4)
```

​		**`arguments`**会一次性接受所有的实参，哪怕已经存在形参

```js
function fn(a, b){
	console.log(a, b)
	console.log(arguments) // arguments会一次性接收所有的实参
}
fn(1, 2, 3, 4)
// 1, 2
// Arguments(4) [1, 2, 3, 4, callee: ƒ, Symbol(Symbol.iterator): ƒ]
```

​		**`arguments.length`**返回实参的个数

```js
function fn(){
	console.log(arguments.length) // arguments.length返回实参的个数
}
fn(1, 2, 3, 4) // 4
```

