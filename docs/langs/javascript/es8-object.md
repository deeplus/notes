# Object拓展

​		es5 引入了**`Object.keys()`**方法，返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键名。

​		es2017 引入了跟**`Object.keys()`**配套使用的**`Object.values()`**和**`Object.entries()`**，作为遍历一个对象的补充手段，供**`for...of`**循环使用。

### Object.keys()

​	返回一个所有元素为**`字符串`**的数组，成员是参数对象自身的（不含继承的）所有可枚举（enumerable）属性的键名。

> 语法：**`Object.keys(obj)`**

```javascript
const alice = {
	name: 'xiaojiao',
	age: 18,
	sex: '女'
}
let obj = Object.keys(alice) // ["name", "age", "sex"]

for (let key of obj) {
	console.log(key)
}
// 'name'
// 'age'
// 'sex'
```

---

### Object.values()

​	返回一个数组，成员是参数对象自身的（不含继承的）所有可枚举（enumerable）属性的键值。

> 语法：**`Object.values(obj)`**

```javascript
const alice = {
	name: 'xiaojiao',
	age: 18,
	sex: '女'
}
let obj = Object.values(alice) //  ["xiaojiao", 18, "女"]

for (let value of obj) {
	console.log(value)
}
// 'xiaojiao'
// 18
// '女'
```

---

### Object.entries()

​	返回一个数组，成员是参数对象自身的（不含继承的）所有可枚举（enumerable）属性的键值对数组。

> 语法：**`Object.entries(obj)`**

```javascript
const alice = {
	name: 'xiaojiao',
	age: 18,
	sex: '女'
}
let obj = Object.entries(alice) 
// [["name", "xiaojiao"], ["age", 18], ["sex", "女"]]

for (let [key, value] of obj) {
	console.log(key, value)
}
// 'name' 'xiaojiao'
// 'age' 18
// 'sex' '女'
```
