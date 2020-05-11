# Iterator

​	**`Iterator`** 函数返回一个对象，它实现了遗留的迭代协议，并且迭代了一个对象的可枚举属性。

### 概念

​	迭代器是一种接口，是一种机制。它能够为不同的数据结构提供统一的访问机制，任何数据结构只要部署**`Iterator`**接口，就可以完成遍历操作（即依次处理该数据结构的所有成员)。

---

### 作用

​	**`Iterator`**的作用有3个：

* 为各种数据结构，提供一个统一的、简便的访问接口；
* 使得数据结构的成员能够按照某种次序排列；
* 主要供**`for...of`**消费。

---

### 本质

​	**`Iterator`**本质上就是一个**`指针对象`**，其过程是这样的：

1. 创建一个指针对象，指向当前数据结构的起始位置；
2. 第一次调用指针对象的**`next()`**方法，可以将指针指向数据结构的第一个成员；
3. 第二次调用指针对象的**`next()`**方法，指针就指向数据结构的第二个成员；
4. 不断地调用指针对象的**`next()`**方法，直到它指向数据结构的结束位置。

---

### Iterator的实现

```js
function mtIter(obj) {
	let i = 0;
	return {
		next() {
			let done = (i >= obj.length);
			let value = !done ? obj[i++] : undefined;
			return {
				value,
				done
			}
		}
	}
}
```

---

### 部署Iterator接口

​	原生具备Iterator接口的数据结构有以下6类：

* **`Array`**

* **`Map`**

* **`Set`**

* **`String`**

* **`arguments对象`**

* **`NodeList对象`**

​	下面的例子是数组的**`Symbol.iterator`**属性。

```javascript
let arr = ['a', 'b', 'c']
let iter = arr[Symbol.iterator]()

iter.next() // {value: "a", done: false}
iter.next() // {value: "b", done: false}
iter.next() // {value: "c", done: false}
iter.next() // {value: undefined, done: true}
```

​	下面是另一个类数组对象调用数组的**`Symbol.iterator`**方法的例子。

```javascript
let iterable = {
	0: 'a',
	1: 'b',
	2: 'c',
	length: 3,
	[Symbol.iterator]: Array.prototype[Symbol.iterator]
};
for (let item of iterable) {
	console.log(item) // 'a', 'b', 'c'
}
```

!> 普通对象部署数组的**`Symbol.iterator`**方法，并无效果。

```js
let iterable = {
	a: 1,
	b: 2,
	c: 3,
	length: 3,
	[Symbol.iterator]: Array.prototype[Symbol.iterator]
};
for (let item of iterable) {
	console.log(item) // 'undefined', 'undefined', 'undefined'
}

/*
*	因为iterator内部的指针对象在自增的时候，如果不是数字，++的时候返回NaN，因此就无法获取到值，所以返回undefined
*/
```

