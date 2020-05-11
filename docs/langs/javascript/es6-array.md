# Array拓展

### 拓展运算符

​	拓展运算符(spread)是三个点**`...`**，它可以在函数调用/数组构造时, 将数组表达式或者string在语法层面展开；还可以在构造对象时, 将对象表达式按key-value的方式展开。

​	拓展运算符好比rest参数的逆运算，将一个数组转为用逗号分隔的参数序列。

>   语法：
>
>   **`[...iterableObj, '4', ...'hello', 6]`**

#### 展开数组

```js
// 展开数组
...[1, 2, 3] // 1 2 3

// 展开字符串
[...[1, 2], '4', ...'hello', 6] // [1, 2, "4", "h", "e", "l", "l", "o", 6]

// 复制数组
var arr = [1, 2, 3]
var arr2 = [...arr]
console.log(
	arr2 // [1, 2, 3]
	arr === arr2 // false
)

// 展开类数组
let box = [...document.getElementsByClassName('box')]

// 拓展运算符后面还可以放置表达式
const arr = [
	...(x > 0 ? ['a'] : []), // 会先计算表达式，再把结果展开
	'b',
]
// 如果x>0,则结果为：['a', 'b']
// 如果x<0,则结果为：['b']

// 如果拓展运算符后面是空数组，则不产生任何效果
[...[], 1] // [1]
```

---

#### 替代数组的apply()方法

​	由于拓展运算符可以展开数组，所以不再需要**`apply()`**方法，将数组转为函数的参数。

```js
// ES5 的写法
function fn(x, y, z) {
	// ...
}
var args = [1, 2, 3]
fn.apply(null, args) 

// ES6 的写法
function fn(x, y, z) {
	// ...
}
var args = [1, 2, 3]
fn(...args)

/*
*		通过Math.max()取数组的最大值
*/

// ES5
Math.max.apply(null, [1, 5, 2, 8]) // 8

// ES6
Math.max(...[1, 5, 2, 8])

// 以上两种方法等同于
Math.max(1, 5, 2, 8)
```

---

#### 拓展运算符的应用

##### 复制数组

```js
// es5
const a1 = [1, 2]
const a2 = a1.concat()


/*
*		拓展运算符提供了复制数组的简便写法
*/

const a1 = [1, 2]

// 写法1
const a2 = [...a1]

// 写法2
const [...a2] = a1
```

---

##### 合并数组

```js
/*
*		拓展运算符提供了数组合并的新写法
*/

var arr1 = ['a', 'b']
var arr2 = ['c']
var arr3 = ['d', 'e']

// es5合并数组
arr1.concat(arr2, arr3) // ['a', 'b', 'c', 'd', 'e']

// es6合并数组
[...arr1, ...arr2, ...arr3] // ['a', 'b', 'c', 'd', 'e']
```

---

##### 与结构赋值结合

```js
/*
*		拓展运算符可以与解构赋值结合起来，用于生成数组
*/

// es5
a = list[0]
rest = list.slice(1)

// es6
[a, ...rest] = slice
```

---

##### 将字符串转为真正的数组

```js
[...'hello']
// ['h', 'e', 'l', 'l', 'o']
```

---

##### 实现了Iterator接口的对象

```js
let nodeList = document.getElementsByClassName('box')
let array = [...nodeList]
```

---

### for...of

​	es6 引入了作为遍历所有数据结构的统一方法。

​	一个数据结构只要具备了**`Symbol.iterator`**属性，就被视为具有**`iterator接口`**，就可以用**`for...of`**循环遍历它的成员。也就是说，**`for...of`**循环内部调用的是**`Symbol.iterator`**方法。

> 语法：
>
> ```javascript
> for (variable of iterable) {
> 	// statements
> }
> ```
>
> variable ：每次迭代中，将不同属性的值分配给变量；
>
> iterable：被迭代枚举其属性的对象。

```javascript
// 迭代数组
let arr = ['a', 'b', 1, 2]
for (let value of arr) {
	console.log(value)
}
// 'a'
// 'b'
// 1
// 2

// 迭代字符串
let str = 'hello'
for (let value of str) {
	console.log(value)
}
// 'h'
// 'e'
// 'l'
// 'l'
// 'o'
```

---

### Array.from()

​	用于将两类对象**`(伪数组对象或可迭代对象)`**转为真正的数组，返回一个新的、浅拷贝的数组实例。

> 语法：**`Array.from(arrayLike[, mapFn[, thisArg]])`**
>
> arrayLike：想要转换成数组的伪数组对象或可迭代对象；
>
> mapFn：可选，类似于数组的**`map`**方法，用来对每个元素进行处理，将处理后的值放入返回的数组中；
>
> thisArg：可选，如果**`map`**函数里用到了**`this`**关键字，就可以传入该参数，用来绑定**`this`**。

```javascript
// nodeList对象
var nodeList = document.querySelectorAll('div')
Array.from(nodeList).forEach(function (p) {
	console.log(p)
})

// arguments对象
function foo() {
	var args = Array.from(arguments)
}
```

---

### Array.of()

​	用于将一组值转换为数组，返回一个新的**`Array()`**实例。这个方法的主要目的，是为了弥补构造函数**`Array()`**的不足。因为参数个数的不同，会导致**`Array()`**的行为有差距（只传一个值，表现形式很奇怪）。

> 语法：**`Array.of(element0[, element1, ...elementN])`**		

```javascript
new Array(10) // [empty × 10]

Array.of(10) // [10]

Array.of() // []
Array.of(1, '2', 3) // [1, '2', 3]
Array.of(undefined, null) // [undefined, null]
```

---

### copywithin() ✵

​	在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原数组），然后返回当前数组。也就是说，该方法会改变源数组。

> 语法：**`array.copyWithin(target[, start[, end]])`**
>
> target：从该位置开始替换数据；
>
> start：可选，从该位置开始读取数据，默认为**`0`**；如果为负数，表示从末尾开始计算；
>
> end：可选，到该位置前停止读取数据，默认为**`array.length`**；如果为负数，表示从末尾开始计算；
>
> 这三个参数必须为整数，如果不是，会自动转为数值。
>
> **`在位置允许的情况下，截取到几个值，就替换几位`**

```javascript
[1, 2, 3, 4, 5].copyWithin(2) // [1, 2, 1, 2, 3], 截取到5个值，从2号位开始替换，替换3位
[1, 2, 3, 4, 5].copyWithin(-2) // [1, 2, 3, 1, 2], 截取到5个值，从-2位开始替换，替换2位
[1, 2, 3, 4, 5].copyWithin(0, 3) // [4, 5, 3, 4, 5], 截取到2个值，从零开始替换，替换2位
[1, 2, 3, 4, 5].copyWithin(-2, -3, -1) // [1, 2, 3, 3, 4]
```

---

### find()

​	用于找出第一个复合条件的数组成员，它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为true的成员，然后返回该成员；如果没有复合条件的成员，则返回**`undefined`**。

> 语法：**`arr.find(callback(element, index, array)[, thisAry])`**
>
> element ：当前元素的值
>
> index ：当前元素的索引
>
> array ：数组本身
>
> thisAry：绑定回调函数的this

```javascript
// find()用于查找满足测试函数的第一个元素的值

[1, 4, -5, 10].find((n) => n < 0) // -5

[1, 5, 10, 15].find(function (v, i, a) {
	return v > 9
}) // 10
```

---

### findIndex()

​	返回数组中满足提供的测试函数的第一个元素的**`索引`**，否则返回**`-1`**。

> 语法：**`arr.findIndex(callback[, thisAry])`**

```javascript
[1, 4, -5, 10].findIndex((n) => n < 0) // 2

[1, 5, 10, 15].find(function (v, i, a) {
	return v > 9
}) // 2
```

---

### fill() ✵

​	用一个固定值填充一个数组中从起始索引到终止索引内的全部元素，不包括终止索引，并将数组返回，该方法**`会改变源数组`**。

​	该方法用于空数组的初始化非常方便，数组中已有的元素，会被全部抹去。

> 语法：**`array.fill(value[, start[, end]])`**
>
> value：用来填充数组元素的值；
>
> start：起始索引，默认为**`0`**；
>
> end：终止索引，默认为**`array.length`**。

```javascript
// 空数组初始化
Array(10).fill(1) // [1, 1, 1, 1, 1, 1, 1, 1, 1, 1]

[1, 2, 3].fill(4) // [4, 4, 4]
[1, 2, 3].fill(4, 1) // [1, 4, 4]
[1, 2, 3].fill(4, 1, 2) // [1, 4, 3]
[1, 2, 3].fill(4, 3, 3) // [1, 2, 3]
[1, 2, 3].fill(4, -3, -2) // [4, 2, 3]

// fill()用于替换数组内的元素
var arr = [1, 2, 3, 4]

// fill with 5 from position2 untill position4
arr.fill(5, 2, 4) // [1, 2, 5, 5]

// fill with 0 form position 1
arr.fill(0, 1) // [1, 0, 0, 0]

// fill with 6 from position 0
arr.fill(6) // [6, 6, 6, 6]
```

---

​		**`entries()`**、**`keys()`**、**`values()`**三者都是用于遍历数组。它们都返回一个遍历器对象，可以用**`for...of`**循环进行遍历，唯一的区别是：**`keys()`**是对**`键名`**的遍历，**`values()`**是对**`键值`**的遍历，**`entries()`**是对**`键值对`**的遍历。

### keys()

​	返回一个包含数组中每个索引键的**`Array Iterator`**对象。

> 语法：**`array.keys()`**

```javascript
let arr = ['a', 'b', 'c', 'd']
let iterator = arr.keys()

for (let key in iterator) {
	console.log(key)
}
// 0
// 1
// 2
// 3
```

---

### values()

​		返回一个新的 **`Array Iterator`** 对象，该对象包含数组每个索引的值。

> 语法：**`array.values()`**

```javascript
let arr = ['a', 'b', 'c', 'd']
let iterator = arr.values()

for (let value of iterator) {
	console.log(value)
}
// 'a'
// 'b'
// 'c'
// 'd'
```

---

### entries()

​	返回一个新的**`Array Iterator`**对象，该对象包含数组中每个索引的键/值对。

> 语法：**`array.entries()`**

```javascript
let arr = ['a', 'b', 'c', 'd']
let iterator = arr.entries()

// 解构赋值
for (let [key, value] of iterator) {
	console.log(key, value)
}
// 0		'a'
// 1		'b'
// 2		'c'
// 3		'd'
```

---

### 数组的空位

​	es6 的方法都不会忽略数组空位，会将空位处理为**`undefined`**。数组的空位指的是：数组的某一位置没有任何值。

​	!> 空位不是**`undefined`**,一个位置的值等于**`undefined`**，依然是有值的，空位是没有任何值，**`in`**操作符可以很好的说明这一点。

```javascript
// 有值
0 in [undefined, undefined, undefined] // true

// 无值 - 空位
0 in [, , ] // false
```

---

#### es5对空位的处理

​	es5 对空位的处理，已经很不一致了，大多数情况下会忽略空位。

*  **`forEach()`**、**`filter()`**、**`reduce`**、**`every()`**和**`some()`**都会跳过空位；

*  **`map()`**会跳过空位，但会保留这个值；

*  **`join()`**和**`toString()`**会将空位视为**`undefined`**，而**`undefined`**和**`null`**会被处理成**`空字符串`**。

---

#### es6对空位的处理

​	ES6则是明确将空位转为**`undefined`**。

* **`Array.from()`**方法会将数组的空位转为**`undefined`**，也就是说：该方法不会忽略空位;

```javascript
Array.from(['a', , 'b']) // ["a", undefined, "b"]
```

* 拓展运算符**`...`**也会将空位转为**`undefined`**;

```javascript
[...['a', , 'b']] // ["a", undefined, "b"]
```

* **`copyWithin()`**会连空位一起拷贝；

```javascript
[, 'a', , 'b'].copyWithin(2, 0) // [empty, "a", empty, "a"]
```

* **`fill()`**会将空位视为正常的数组位置；

```javascript
new Array(3).fill(3) // [3, 3, 3]
```

* **`for...of`**循环也会遍历空位；

```javascript
let arr = [, , ,]

for (let key of arr) {
	console.log(1)
}
// 1
// 1
// 1

/*
*		上面的代码中，数组arr有三个空位，for...of并没有忽略它们，如果改为map()，空位是会跳过的。
*/
```

* **`keys()`**、**`values()`**、**`entries()`**、**`find()`**和**`findIndex()`**会将空位处理为**`undefined`**。

```javascript
// keys()
[...[, 'a'].keys()] // [0, 1]

// values()
[...[, 'a'].values()] // [undefined, "a"]

// entries()
[...[, 'a'].entries()] 
/*
	(2) [Array(2), Array(2)]
		0: (2) [0, undefined]
		1: (2) [1, "a"]
		length: 2
	__proto__: Array(0)
*/

// find()
[, 'a'].find(x => true) // undefined

// findIndex()
[, 'a'].findIndex(x => true) // 0
```

​		由于空位的处理规则非常不统一，所以建议避免出现空位。

​	

