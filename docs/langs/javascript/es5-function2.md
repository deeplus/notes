# Function对象

​	函数的**`call()`**、**`apply()`**、**`bind()`**都能用于修改函数**`this`**的指向。它们的区别在于：**`call`**和**`apply`**会主动执行调用函数，而**`bind`**不会主动执行调用函数，并且**`bind不兼容低版本IE`**。

### call()

​	接收一个**`参数列表`**和一个指定的**`this`**值来调用一个函数。

> 语法：
>
> ```css
> function.call(thisAry, arg1, arg2, ..., argX)
> ```
>
> 参数：
>
> * **`thisAry`**(可选)：**`function`**函数运行时使用的**`this`**值；
>
> * **`arg`**(可选)：参数列表。
>

```javascript
var a = 1
var obj = {
	a: 2
}

function fn(a, b, c) {
	console.log(this.a)
	console.log(a + b + c)
}

fn(1, 2, 3) // 1  6, fn自执行this指向顶层对象
fn.call(obj, 1, 2, 3) // 2  6, call()修改fn的this指向obj
```

---

### apply()

​	接收一个**`包含多个参数的数组(或类数组对象)`**和一个指定的**`this`**值来调用一个函数。

> 语法：
>
> ```css
> function.apply(thisArg[, argsArray])
> ```
>
> 参数：
>
> * **`thisAry`**(可选)：**`function`**函数运行时使用的**`this`**的值；
>
> * **`argsArray`**(可选)：一个数组或者类数组对象，其中的数组元素将作为单独的参数传给**`function`**函数。如果该参数的值为**`null`**或**`undefined`**，则表示不需要传入任何参数。
>

```javascript
var a = 1
var obj = {
	a: 2
}

function fn(a, b, c) {
	console.log(this.a)
	console.log(a + b + c)
}

fn(1, 2, 3) // 1  6, fn自执行this指向顶层对象
fn.apply(obj, [1, 2, 3]) // 2  6, apply()修改fn的this指向obj
```

---

### ☂ bind()

​	创建一个新的函数，在**`bind()`**被调用时，这个新函数的**`this`**被指定为**`bind()`**的第一个参数，而其余参数将作为新函数的参数，供调用时使用。

​		**`bind`**的返回值是原函数的拷贝，也就意味着**`bind`**需要手动执行。

> 语法：
>
> ```css
> function.bind(thisArg, arg1, arg2, ..., argX)
> ```
>
> 参数：
>
> * **`thisAry`**(可选)：调用绑定函数时作为**`this`**参数传递给目标函数的值；
>
> * **`arg`**(可选)：当目标函数被调用时，被预置入绑定函数的参数列表中的参数。
>

```js
var a = 1
var obj = {
	a: 2
}

function fn(a, b, c) {
	console.log(this.a)
	console.log(a + b + c)
}

fn(1, 2, 3) // 1  6, fn自执行this指向顶层对象
fn.bind(obj, 1, 2, 3)() // 2  6, bind()修改fn的this指向obj
```

```js
// bind()方法不兼容低版本ie

Function.prototype.bind = function () {
	// 实参的第一项为内层apply函数的this指向
	var bindThis = arguments[0]
    
	// 实参的第二到最后一项为内层apply函数的实参，但arguments对象是一个类数组对象，要想使用slice，需要将arguments对象转为一个数组对象
	// slice的内部其实是对this（内层this代表数组实例）进行遍历，如果修改this指向arguments，则arguments就变成了一个数组对象
	var args = Array.prototype.slice.call(arguments, 1)
    
	// 当前this指向数组实例
	var that = this
    
	return function () {
		that.apply(bindThis, args)
	}
}
```



