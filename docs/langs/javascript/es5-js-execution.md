# JavaScript的执行

### 编译期

编译期会对代码进行**`静态分析`**，包括词法分析、语法分析和代码生成，主要找声明的变量、函数，检查语法是否符合规范。

*   **`词法分析`**：将字符串分解为有意义的代码块（**`词法单元`**）;
*   **`语法分析`**：将词法单元流转换为一个由元素嵌套的程序语法树（抽象语法树，**`AST`**）;
*   **`代码生成`**：这个阶段也叫做**`预编译`**，主要是将AST转换为可执行代码。**`该阶段存在变量提升`**。

!> &emsp;&emsp;函数作为JavaScript的一等公民，如果在同作用域出现函数声明和var关键字声明变量名冲突时，在编译期**`function会覆盖var声明的变量名`**，而let声明不会出现这种情况，因为let不允许重复声明。

---

### 执行期

​	执行期则正常执行编译好的代码。

```js
console.log(a) //f a(){}
function a() {}
var a = 123
console.log(a) // 1

/*
* @ var声明变量与function声明变量冲突，function覆盖var
* @ 编译期：
	function a(){} -->声明a并绑定全局作用域
	var a = undefined --> 声明一个变量a，绑定全局作用域并初始化值undefined
	--->同一作用域函数声明与var声明冲突，function覆盖var 
* @ 执行期：
	console.log(a) // f a(){}
	a = 123
	console.log(a) // 123
*/
```

---

### TDZ

​	**`TDZ`**即变量的**`暂时性死区`**（全称Temporal Dead Zone），**`TDZ并不是某个地方，或是内存中的某个区域，而是指变量被声明和被初始化之间的这段时间，TDZ只存在于es6声明变量的关键字中`**。

​	**`TDZ`**的本质：只要一进入当前作用域，所要使用的变量就已经存在了，但是不可获取，只有等到声明变量的那一行代码出现，才可以获取和使用该变量。

```js
// 使用var声明的变量由于存在变量提升，在没有声明之前使用不会报错
console.log(a) // undefined
var a = 1
console.log(a) // 1

/*
* @ 由于var关键字存在变量提升，所以以上代码的实际运行为：
* @ 编译期：var a = undefined -->声明一个变量a，给a绑定一个全局作用域并初始化一个值undefined
* @ 执行期：
*	console.log(a) // undefined
*	a = 1
*	console.log(a) // 1
*/
```

```js
// 使用let声明的变量不存在变量提升，并且受死区的影响，在没有声明之前使用，就会报错
// ReferenceError: Cannot access 'a' before initialization

console.log(a)

// 从被声明到被赋值之前的区域，被称作变量a的暂时性死区
let a = 123
console.log(a) 

/*
* @ 由于let不存在变量提升，所以以上代码的实际执行顺序：
* @ 编译期：let a -->声明一个变量a，给a绑定一个全局作用域并赋值undefined
* @ 执行期： 
*	console.log(a) //	在当前作用域，变量a已经存在，但此时由于处在变量a的暂时性死区，不能访问a，于是报错ReferenceError，终止后续代码执行
*/
```

```js
let a = 1
function fn(a = a) {
	console.log(a)
}
fn()
//  ReferenceError: Cannot access 'a' before initialization

/*
* @ 输出结果为什么不是1而是报错
* @	原因：
*   当函数的形参有默认值的时候，函数的()会产生一个临时的作用域，由于函数的形参是es6新增的，所以函数的声明在使用时就相当于默认使用let来声明，即(let a = a)
	在编译期： let a --> 声明一个变量a并绑定作用域()
	执行期： a = a -->a未声明就使用，出于a的暂时性死区，抛出错误
*/
```

