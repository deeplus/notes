# 解构赋值

​	es6 允许按照一定的模式，从数组和对象中提取值，对变量进行赋值，这被称为**`解构赋值(Destructuring)`**。解构赋值语法是 JavaScript 的一种表达式，可以方便的从数组或者对象中快速提取值赋给定义的变量。

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

