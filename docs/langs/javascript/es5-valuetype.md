# 引用类型和值类型

### 引用型数据

​	即复杂的object，包括：**`function`**、**`[]`**和**`{}`**。

​	引用型数据在比较时是比较对象的**`内存地址`**，内存地址相同，则相等。

```js
// 引用型数据比较的是内存地址
var s1 = []
var s2 = []

// 内存地址不同，则值不相等
s1 === s2 // false

// 内存地址相同，则值相等
var s3 = s1 // -> 将s1的内存地址指向s3
s1 === s3 // true

// 此时修改s1的值，则s3也改变
s1[0] = 1
console.log(s3) // [1]
```

```js
// 示例1
function fn() {
	console.log(this)
}
var obj = {
	a: fn
}
var f = obj.a // obj.a即函数的地址，该方式相当于交出函数的内存地址

obj.a() // obj --> 这种方式需要访问对象的属性，依赖于对象
f() // window --> 相当于fn调用
```

```js
// 示例2
function fn() {
	console.log(this)
}
var obj = {
	a: fn
}
var f = obj.a
function f2(a) {
	a() // window --> 本次调用不依赖于obj
	arguments[0]() // arguments --> 理解：arguments = [0: fn的内存地址] 
}
function f3(...a) {
	a[0]() // [f]
}
f2(obj.a) // -->传入的是fn的内存地址
```

---

### 值类型数据

​	包括：**`number`**、**`boolean`**、**`string`**、**`null`**和**`undefined`**

​	值类型数据在比较时只会比较两个数据是否长的一样。

```javascript
// 值类型数据只会比较是否长的一样
var s1 = '123'
var s2 = '123'
s1 === s2 // true
```

