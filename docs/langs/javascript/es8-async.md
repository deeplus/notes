# async函数

​	es2017 引入了**`async`**函数，使得异步操作变得更加方便。

​	**`async`**函数是**`Grnerator`**函数的语法糖，是基于**`Generator`**和**`Promise`**的封装：**`async`**函数使用时就是将**`Generator`**函数的**`*`**替换成**`async`**，将**`yield`**替换成**`await`**，仅此而已。

### 语法糖

​	**`语法糖`**意指那些没有给计算机语言添加新功能，而只是对人类来说更“甜蜜”的语法。语法糖往往给程序员提供了更甜蜜的编码方式，有益于更好的编码风格、更易读，不过其并没有给语言添加什么新东西。

​	反向还有**`语法盐`**：

​	主要目的是通过反人类的语法，让你更痛苦的写代码。虽然同样能够达到避免代码书写错误的效果，但是编程效率很低，毕竟提高了语法学习门槛，让人齁到忧伤...

---

### async与Generator的区别

1.  内置执行器：**`Generator`**函数的执行必需依靠执行器，而**`async`**函数自带执行器。也就是说：**`async`**函数的执行与普通函数一模一样，只需要一行；
2.   更好的语意：**`async`**和**`await`**，比起**`*`**和**yield**，语意更清楚了。**`async`**表示函数里有异步操作，**`await`**表示紧跟在后面的表达式需要等待结果；
3.   正常情况下，**`await`**命令后面是一个**`Promise`**对象。如果不是，会被转成一个立即**`resolve`**的**`Promise`**对象。

---

### 定义一个async函数

> 语法：
>
> ```javascript
> async function [name](param1[, param2[, ...paramN]) {statements}
> ```
>
> 参数：
>
> * **`name`**(可选)：异步函数的名称，可以省略，如果省略该函数就称为一个匿名函数；
>
> * **`paramN`**(可选)：形参；
>
> * **`statements`**：组成函数体的语句。

```javascript
async function fn() {
	var res = await 20
	console.log(res)
}
fn() // 20
```

---

### await

​	await`** 操作符用于等待一个**`Promise`**对象，并返回**`Promise`**对象的处理结果。

> 语法：
>
> ```javascript
> [return_value] = await expression
> ```
>
> 参数：
>
> * **`expression`**：一个表达式，可以是Promise对象或任何要等待的值。
>
> * **`return_value`**：一个返回值。如果**`await`**后面的表达式是一个**`Promise`**对象，则返回Promise对象的处理结果；如果**`await`**后面的表达式不是一个**`Promise`**对象，则返回该值本身。

```javascript
async function fn() {
	var x = await setTimeout(() => {                
	}, 2000)
  
	console.log(x)
}
fn() // 1, 定时器的id值
```

---

### 错误处理

​	**`await`** 表达式会暂停当前**`async function`**的执行，等待 Promise 处理完成。

​	若 Promise 正常处理(fulfilled)，其回调的resolve函数参数作为 **`await`** 表达式的值，继续执行 **`async function`**。

```javascript
async function fn() {
	var x = await new Promise(resolve => {
		setTimeout(() => {
			resolve('异步1要返回的数据')
		}, 2000)
	})
	console.log(x)
} 
fn() // '异步1要返回的数据'
```

​	若 Promise 处理异常(rejected)，**`await`** 表达式会把 Promise 的异常原因抛出。此时为了防止出错，可以把语句放在**`try...catch`**中。

```javascript
async function fn() {
	try {
		var res = await Promise.reject('异步1返回的错误信息')
	} catch (err) {
		console.log(err)
	}
}
fn() // '异步1返回的错误信息'
```



​	