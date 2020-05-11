# Function拓展

### 函数参数默认值

​	es6 支持定义函数的时候为其设置**`默认值`**，当某次传入的实参个数少于形参个数时，默认值生效。

​	默认值生效的原理：检测形参接收到的值是否为**`undefined`**，如果为**`undefined`**，则抛弃undefined使用**`默认值`**

```javascript
// 函数参数默认值
function fn(a = 2, b = 2) {
	console.log(a + b)
}
fn(1, 2) //3
fn(2) // 4	b = 2生效
fn() // 4	a = 2，b = 2生效
```

​	**`果函数有多个参数，要把带默认值的参数放后边，不带默认值的参数放前边`**

```javascript
function(a, b, c = 1) {
	console.log(a + b - c)
}
fn(1, 2, 3) //0
fn(1, 2) // 2
```

​	**`函数初始化时，如果函数参数有默认值，那么函数的圆括号会产生一个临时的作用域，这个作用域在函数初始化结束后销毁`**。

```javascript
let a = 1
function fn(a = a) { // 由于圆括号会产生一个临时作用域，所以此时还处于a的暂时性死区，不要期望默认值a能够取到1
	
}
fn() // Uncaught ReferenceError: Cannot access 'a' before initialization
```

​	函数参数默认值与**`结构赋值`**结合使用

```javascript
function fn({a, b = 5}) {
	console.log(a, b)
}
fn({}) // undefined 5
fn({a: 1}) // 1 5
fn({a: 1, b: 2}) // 1 2
```

---

### 函数新属性

#### name

​	函数的name属性返回函数名。

```javascript
function sayName() {
	console.log(sayName.name) // name属性返回函数名
}
sayName() // sayName
```

---

#### length

​	函数的length属性返回函数的形参个数，但是返回值不包括带默认值的形参，也不包括剩余参数。

```javascript
function fn(a, b, c) {
	console.log(fn.length) // length属性返回形参个数
}
fn(1, 2, 3, 4) // 3

// length属性不包括带默认值的形参和rest参数
function fn(a, b, c = 1, ...d){
	console.log(fn.length) 
}
fn(1, 2, 3, 4) // 2
```

---

### 临时作用域

​	函数参数一旦设置了默认值，函数进行声明初始化时，参数会形成一个单独的作用域，等到初始化结束，这个作用域就会消失。这种行为，在不设置参数默认值时，是不会出现的。

```javascript
/*
*		在下面的代码中：参数y的默认值等于变量x，调用函数fn时，参数形成一个单独的作用域，在这个作用域里边，默认值变量x指向第一个参数x，而不是全局变量x，所以当不传值时输出undefined，传值时输出2
*/

var x = 1
function fn(x, y = x) {
	console.log(y)
}

fn() // undefined
fn(2) // 2

/*
*		在下面的代码中：函数fn调用时，参数y = x形成一个单独的作用域，这个作用域里边，变量x本身没有定义，所以指向外层的全局变量x。函数调用时，函数体内部的局部变量x影响不到默认值变量x。
*/

let x = 1
function fn(y = x) {
	let x = 2
	console.log(y)
}
fn() // 1

/*
*		在下面的代码中：参数x = x形成一个单独的作用域。实际执行的是let x = x，由于暂时性死区的缘故，这段代码会报错。
*/

var x = 1
function fn(x = x)	{
	// code...
}
fn() // Uncaught ReferenceError: Cannot access 'a' before initialization

/*
*		下面的代码中：如果将var x = 3中的var去除，函数fn的内部变量x就指向第一个参数x，与匿名函数内部的x是一致的，所以最后输出的就是2，而外层的全局变量x依然不受影响。
*/

var x = 1
function fn(x, y = function () {x = 2}) {
	var x = 3
	y()
	console.log(x)
}
fn() // 3
x // 1

// 去除var
var x = 1
function fn(x, y = function () {x = 2}) {
	x = 3
	y()
	console.log(x)
}
fn() // 2
x // 1
```

---

### rest参数

​	**`rest参数`**的形式为**`...变量名`**，rest参数用于获取函数的多余参数，这样就不需要使用arguments对象。rest参数搭配的是一个**`数组`**，只会将那些**`没有对应形参的实参`**放到数组中。

```javascript
function fn(a, ...b) {
	console.log(a) 
	console.log(b) // 函数的rest参数只会接收那些没有对应形参的实参
}
fn(1, 2, 3, 4)
// 1
// [2，3，4]
```



​		需要注意的是，一个函数只能有一个剩余参数，所以剩余参数必须写在最后，否则报错。

```javascript
function fn(...a,  b) {
	console.log(a)
	console.log(b)
}
fn(1, 2, 3, 4)
// Uncaught SyntaxError: Rest parameter must be last formal parameter
```

---

### 箭头函数

​	es6 允许使用**`箭头( => )`**定义函数。

#### 单条语句

```js
// 只有一条语句
let add1 = function (a) {
	return a + 1
}

// 改写为箭头函数
let add1 = (a) => a + 1

// 如果只有一个形参，可以不加圆括号
let add1 = a => a + 1
```

---

#### 多条语句

```js
// 当有多条语句时
let add2 = function fn(v) {
	let a = v + 2
	let c = a * 5
	return c
}

// 改写为箭头函数
let add2 = (v) => {
	let a = v + 2
	let c = a * 5
	return c
}
```

---

#### 默认返回值

​	当箭头函数有多条语句时，如果不显示return一个值，则默认返回**`undefined`**。

```javascript
// 箭头函数默认return undefined
let fn = (n) => {
	let a = n + 1
	let b = a * 2
}
fn(2) // undefined
```

---

#### this

​	箭头函数的**`this`**是固化的(指向所在环境的this)，或者说箭头函数压根**`没有this`**，所以在箭头函数里使用**`this`**，是默认使用**`外层的this`**。

```javascript
let fn = () => {
	console.log(this)
}
fn() // window
this // window
```

​	箭头函数转成es5的代码如下：

```javascript
// es6
function foo() {
	setTimeout(() =>{
		console.log('id', this.id)
	}, 100)
}

// es5
function foo() {
	var _this = this
	setTimeout(function() {
		console.log('id', _this.id)
	}, 100)
}
// 转换后的es5版本清楚的说明了，箭头函数里边根本没有自己的this，而是引用外层的this
```

---

### arguments

​	箭头函数**`没有arguments`**。

!> 使用箭头函数必须注意以下几点：<br>&emsp;&emsp;1.  函数体内的**`this`**对象，就是定义时所在的环境，而不是使用时所在的环境；<br>&emsp;&emsp;2. 不可以当作构造函数，也就是说不能通过**`new`**来执行，否则会抛出一个错误；<br>&emsp;&emsp;3. 不可以使用**`arguments`**对象，该对象在函数体内不存在。如果要用，可以用**`rest`**参数代替；<br>&emsp;&emsp;4. 不可以使用**`yield`**命令，因此箭头函数不能用做**`Generator`**函数；<br>&emsp;&emsp;5. 由于箭头函数没有自己的this，自然也就不能用**`call()`**、**`bind()`**、**`apply()`**去改变**`this`**的指向。

 