# 解构赋值

​	es6 允许按照一定的模式，从数组和对象中提取值，对变量进行赋值，这被称为**`解构赋值(Destructuring)`**。解构赋值语法是 JavaScript 的一种表达式，可以方便的从数组或者对象中快速提取值赋给定义的变量。

```js
let {x, y, ...z} = {x: 1, y: 2, a: 3, b: 4}
x // 1
y //  2
z // {a: 3, b: 4}
```

​	由于解构赋值要求等号右边是一个对象，所以如果等号右边是**`undefined`**和**`null`**，就会抛出错误，因为它们无法转为对象。

```js
let {x, y, ...z} = undefined 
// Cannot destructure property 'x' of 'undefined' as it is undefined.

let {x, y, ...z} = null
// Cannot destructure property 'x' of 'null' as it is null.
```

​	解构赋值必须是最后一个参数且只能有一个，否则会报错。

```js
let {...x, y, z} = {x: 1, y: 2, z: 3}
// Rest element must be last element

let {x, ...y, ...z} = {x: 1, y: 2, z: 3}
// Rest element must be last element
```

!> 解构赋值的拷贝是浅拷贝，即如果一个键的值是复合类型的值（数组、对象、函数），那么解构赋值拷贝的是这个值的引用，而不是这个值的副本。

```js
let obj = {a: {b: 1}}
let {...x} = obj

obj.a.b = 2
x.a.b // 2
```

---

### 获取数组中的值

​	从数组中获取值并赋值到变量中，变量的顺序与数组中对象顺序对应。

```javascript
// 一维数组
let [a, b, c, d] = [1, 2, 3, 4]
console.log(
	a, // 1
	b, // 2
	c, // 3
	d  // 4
)

// 多维数组
let [a, b, [c]] = [1, 2, [3]]
console.log(
	a, // 1
	b, // 2
	c  // 3
)
```

​	当左右两边的值不完全对应时，叫做不完全解构，找不到的值就取**`undefined`**。

```javascript
// 不完全解构

// 左边多右边少
let [a, b, c] = [1, 2]
console.log(
	a, // 1
	b, // 2
	c  // undefined
)

// 左边少右边多
let [a, b] = [1, 2, 3]
console.log(
	a, // 1
	b  // 2
)

// ...剩余参数
let [a, b, ...c] = [1, 2, 3, 4]
console.log(
	a, // 1
	b, // 2
	c  // [3, 4]
)

// 每个,代表一位
let [a,, b] = [1, 2, 3, 4]
console.log(
	a, // 1
	b  // 3
)

let [a,,, b] = [1, 2, 3, 4]
console.log(
	a, // 1
	b // 4
)
```

---

### 获取对象中的值

```js
const student = {
	name: 'xiaojiao',
	age: 18,
	sex: '女'
}

// 可以这么写
const {name: name, age: age, sex: sex} = student
console.log(
	name, // 'xiaojiao'
	age, // 18
	sex  // '女'
)

// 上述方式可以简写为
const {name, age, sex} = student
console.log(
	name, // 'xiaojiao'
	age, // 18
	sex  // '女'
)
```

