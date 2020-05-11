# Generator

​	**`Generator`**函数是es6提供的一种异步编程解决方案，语法行为与传统函数完全不同。

​	执行**`Generator`**函数会返回一个遍历器对象。也就是说：**`Generator`**还是一个遍历器对象生成函数。返回的遍历器对象，可以依次遍历**`Generator`**函数内部的每一个状态。

### 定义一个Generator函数

> 语法：
>
> ```javascript
> // 分步执行函数
> function* generator() {
> 	yield 1;
> 	yield 2;
> 	yield 3;
> }
> let g = generator() // Generator {}
> ```
>
> 星号的位置：
>
> * **`*`**只要在**`function`**声明和函数名之间就行，位置任意。

```javascript
function* helloWorldGenerator() {
	yield 'hello';
	yield 'world';
	return 'ending'
}
let hw = helloWorldGenerator() // Generator { }

/*
*	上面的代码定义了一个Generator函数helloWorldGenerator，它内部有两个yield表达式，即该函数有三个状态：hello、world和return（结束语句执行）。

*	调用Generator函数后，该函数并不执行，返回的也不是运行结果，而是一个指向内部状态的指针对象。也就是上一章介绍的遍历器对象。

*	下一步必须调用遍历器对象的next方法，使得指针移向下一个状态。也就是说，每一次调用next方法，内部指针就从函数头部或上一次停下来的地方开始执行，直到遇到下一个yield表达式（或者return语句）为止。换言之，Generator函数是分段执行的，yield表达式是暂停执行的标记，而next方法可以恢复执行。
*/
```

---

### yield

​		由于**`Generator`**函数返回的遍历器对象，只有调用**`next()`**方法才会遍历下一个内部状态，所以其实提供了一种可以暂停执行的函数。**`yield`**表达式就是暂停标志，用来暂停一个生成器函数。

> 语法：
>
> ```javascript
> [rv] = yield [expression]
> ```
>
> 参数：
>
> * **`rv`**：返回传递给生成器的**`next()`**方法的可选值，以恢复其执行。
> * **`expression`**：定义通过**`迭代器协议`**从生成器函数返回的值。如果省略，则返回undefined。

#### 关于yield

* **`yield`**关键字使生成器函数执行暂停，**`yield`**关键字后面的表达式的值返回给生成器的调用者。它可以被认为是一个基于生成器的版本的**`return`**关键字。

* **`yield`**关键字实际返回一个**`IteratorResult`**对象，它有两个属性，**`value`**和**`done`**。**`value`**属性是对**`yield`**表达式求值的结果，而**`done`**是**`false`**，表示生成器函数尚未完全完成。

* 一旦遇到**`yield`** 表达式，生成器的代码将被暂停运行，直到生成器的**`next()`**方法被调用。每次调用生成器的**`next()`**方法时，生成器都会恢复执行。

* 如果将参数传递给生成器的**`next()`**方法，则该值将成为生成器当前**`yield`**操作返回的值。

---

#### 与return的区别

* 相同点

​		**`yield`**表达式和**`return`**语句都能返回紧跟在语句后面的那个表达式的值；

* 不同点

1. 每次遇到**`yield`**函数就暂停执行，下一次再从该位置继续往后执行，而**`return`**语句不具备位置记忆的功能；

2. 一个函数里面，只能执行一次**`return`**语句，但是可以执行多次**`yield`**表达式。

---

#### 注意

1. **`yield`**表达式只能用在**`Generator`**函数里，用在其它地方都会报错；

2. **`yield`**表达式如果用在另外一个表达式中，必须放在**`()`**里边。

```javascript
// 错误写法
console.log('hello' + yield 123) // SystaxError

// 正确写法
console.log('hello' + (yield 123))
```

---

### yield*

​	如果在**`Generator`**函数内部调用另外一个**`Generator`**函数，默认是没有效果的。

```javascript
function* foo() {
	yield 'a'
	yield 'b'
}

function* bar() {
	yield 'x'
	foo()
	yield 'y'
}

for (let v of bar()) {
	console.log(v)
}
// 'x'
// 'y'
```

​	**`foo`**和**`bar`**都是Generator函数，在**`bar`**里边调用**`foo`**是不会有效果的，这时就需要用到**`yield*`**表达式，用来在一个Generator函数里执行另外一个Generator函数。

```javascript
function* bar() {
	yield 'x'
	yield* foo()
	yield 'y'
}

// 等同于
function* bar() {
	yield 'x'
	yield 'a'
	yield 'b'
	yield 'y'
}

```

---

###  * 位置

​	es6 没有规定**`function`**关键字和函数名之间的**`*`**写在哪个位置，这导致下面的写法都能通过：

```javascript
function* gen(x, y) {/*...*/} // 推荐

function *gen(x, y) {/*...*/}

function * gen(x, y) {/*...*/}

function*gen(x, y) {/*...*/}
```

---

### 方法

​	**`Generator`**函数原生提供3个方法：

#### next()

​		遍历器对象的**`next()`**方法的运行逻辑如下：

1. 遇到**`yield`**表达式，就暂停执行后面的操作，并将紧跟在**`yield`**后面的那个表达式的值，作为返回的对象的**`value`**属性值；

2. 下一次调用**`next()`**方法时，再继续往下执行，直到遇到下一个**`yield`**表达式；

3. 如果没有再遇到新的**`yield`**表达式，就一直运行到函数结束，直到**`return`**语句为止，并将**`return`**语句后面的表达式的值，作为返回的对象的**`value`**属性值。

4. 如果该函数没有**`return`**语句，则返回的对象的**`value`**属性值就为**`undefined`**。

5. 如果在某次调用**`next()`**方法将一个**`yield`**后面的表达式的值返回，如果在下次调用**`next()`**时不进行传值，则该表达式的值在本次调用时就为**`undefined`**；如果进行传值，则该表达式的值就为本次传入的值。

---

#### return()



---

#### throw()



---

### next()的参数

​	**`yield`**表达式本身没有返回值，或者说总是返回**`undefined`**。**`next()`**可以带一个参数，该参数就会被当作上一个**`yield`**表达式的返回值。

```javascript
function* f() {
	for (var i = 0; true; i++){
		var reset = yield i
		if (reset) {i = -1}
	}
}
var g = f()

g.next() // {value: 0, done: false}
g.next() // {value: 1, done: false}
g.next() // {value: 2, done: false}
```

​	这个功能具有很重要的语法意义：**`Generator`**函数从暂停状态到恢复运行，它的上下文状态（context）是不变的，通过**`next`**方法的参数，就有办法在**`Generator`**开始运行之后，继续向整体内部注入值。

```javascript
function* foo(x) {
	var y = 2 * (yield (x + 1))
	var z = yield (y / 3)
	return (x + y + z)
}
var a = foo(5) 
a.next() // {value: 6, done: false}
a.next() // {value: NaN, done: false}
a.next() // {value: NaN, done: true}

var b = foo(5)
b.next() // {value: 6, done: false}
b.next(12) // {value: 8, done: false}
b.next(13) // {value: 42, done: true}
```

---

### for...of循环

​	**`for...of`**循环可以自动遍历**`Generetor`**函数执行时生成的**`Iterator`**对象，且此时不在需要调用**`next()`**。

```javascript
function* foo() {
	yield 1
	yield 2
	yield 3
	yield 4
	return 5
}
for (let v of foo()) {
	console.log(v)
}
// 1, 2, 3, 4
```

```js
function* fibonacci() {
	let [prev, curr] = [1, 1]
	while (true) {
		[prev, curr] = [curr, prev + curr]
		yield curr
	}
}

for (let n of fibonacci()) {
	if (n > 5) break
	console.log(n)
}
// 2, 3, 5
```

---

### 与普通函数的区别

1. **`function`**关键字与函数名之间有一个**`*`**；
2. 函数体内部使用**`yield`**表达式，定义不同的内部状；
3. **`Generator`**函数不能和**`new`**一起使用，会报错。
4. 普通函数只能返回一个值，因为**`return`**只能执行一次。而**`Generator`**函数由于有**`yield`**的存在，可以返回一系列的值。

---

### 与Iterator的关系

​	由于**`Generator`**函数就是遍历器生成函数，因此可以把**`Generator`**赋值给对象的**`Symbol.iterator`**属性，从而使得该对象具有**`iterator`**接口。

```javascript
Object.prototype[Symbol.iterator] = function* () {
	for (let i in this) {
		yield this[i]
	}
}

// =========================
function* iterEntries(obj) {
	let keys = Object.keys(obj)
	for (let i = 0; i < keys.length; i++) {
		let key = keys[i]
		yield [key, obj[key]]
	}
}

let myObj = {
	foo: 3,
	bar: 7
}

for (let [key, value] in iterEntries(myObj)) {
	console.log(key, value)
}
```





