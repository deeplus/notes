# Object的拓展

### 方法

​	es5 在判断两个值是否相等时，只有**`==`**和**`===`**，但是它们都有缺点：前者会自动转换数据类型，后者的**`NaN`**不等于自身，以及**`+0`**等于**`-0`**。JavaScript缺乏一种运算，在所有环境中，只要两个值是一样的，它们就像等。

​	es6 提出同值相等算法，用来解决这个问题。**`Object.is()`**就是部署这个算法的新方法，它用来比较两个值是否严格相等，与严格比较运算符**`===`**的行为基本一致。

#### Object.is()

​	用于判断两个值是否相等。

> 语法：
>
> ```css
> Object.is(value1, value2)
> ```
>

```javascript
Object.is('foo', 'foo') // true

Object.is({}, {}) // false

/*
*		不同之处有两个：+0 ！=== -0；NaN === NaN
*/

Object.is(+0, -0) // false
Object.is(NaN, NaN) // true
```

---

#### Object.assign()

​	用于对象的合并，将一个或多个源对象（source）的所有可枚举（可遍历）属性，复制到目标对象并将其返回。

> 语法：**`Object.assign(target, ...source)`**

```javascript
/*
*		合并对象，目标对象自身会改变
*/ 
const obj1 = {a: 1}
const obj2 = {b: 2}
const obj3 = {c: 3}

// 方法1: 
const obj4 = Object.assign({}, obj1, obj2, obj3) // {a: 1, b: 2, c: 3}

// 方法2:
const obj5 = Object.assign(obj1, obj2, obj3) // {a: 1, b: 2, c: 3}
obj1 // {a: 1, b: 2, c: 3} ,注意目标对象自身也会改变
```

!> 在合并具有相同属性的对象时，属性会被后续参数中具有相同属性的其他对象覆盖。

```js
const o1 = {a: 1, b: 1, c: 1}
const o2 = {b: 2, c: 2}
const o3 = {c: 3}

const obj = Object.assign(o1, o2, o3) // {a: 1, b: 2, c: 3}
```

​	如果只写了一个参数，则**`Object.assign()`**会直接返回该参数。

```js
const obj = {a: 1}
Object.assign(obj) // {a: 1}
```

​	由于**`undefined`**和**`null`**无法转为对象，所以如果它们作为参数，就会抛出错误。

```js
Object.assign(undefined) 
Object.assign(null) 
// Uncaught TypeError: Cannot convert undefined or null to object at Function.assign (<anonymous>)
```

!> **`Object.assign()`**可以用来处理数组，但是会把数组视为对象。

```js
/*
*		下面的代码中，把数组视为了属性为0，1，2的对象，因此源数组的0号属性4覆盖了目标数组的0号属性1
*/

Object.assign([1, 2, 3], [4, 5]) // [4, 5, 3]
```

---

### 属性的简洁表示法

​	es6 允许我们在设置一个对象的属性时不指定属性名，可以直接写入变量和函数，作为对象的属性和方法。

```javascript
/*
*		对象的属性可以简写
*/

// es5
const name = 'alice',
	age = 18,
	sex = '男'
const student = {
	name: name,
	age: age,
	sex: sex
}
console.log(student) // {name: "alice", age: 18, sex: "男"}

// es6
const name = 'alice',
	age = 18,
	sex = '男'
const student = {
	name,
	age,
	sex
}
console.log(student) // {name: "alice", age: 18, sex: "男"}


/*
* 		对象的方法同样能够简写
*/

// es5
const teacher = {
	name: 'rabbit',
  
	introduceMyself: function () {
	console.log(`我的名字叫${this.name}`)
	}
}
teacher.introduceMyself() // 我的名字叫rabbit

// es6
const teacher = {
	name: 'rabbit',
  	
	introduceMyself () {
		console.log(`我的名字叫${this.name}`)
	}
}
teacher.introduceMyself() // 我的名字叫rabbit
```

---

### 属性名表达式

​	JavaScript定义对象的属性，有两种方法。

```javascript
const object = {}

// 方法1
object.name = 'bixiao' // {name: "bixiao"}

// 方法2
object['ya' + 'mo'] = 'yuntian' // {yamo: "yuntian"}
```

​	但是，如果使用字面量的方式（使用花括号）定义对象，在ES5中只能使用方法一（标识符）定义属性。

```javascript
const object = {
	name: 'bixiao',
	yamo: 'yuntian'
}
object // {name: "bixiao", yamo: "yuntian"}
```

​	es6 允许字面量定义对象时，用方法二（表达式）作为对象的属性名，即把表达式放在方括号内。

```javascript
let propKey = 'name'
const object = {
	[propKey]: 'bixiao',
	['ya' + 'mo']: 'yuntian'
}
object // {name: "bixiao", yamo: "yuntian"}
```

​	表达式还可以用于定义方法名。

```javascript
const object = {
	['say' + 'Hello']() {
		console.log('hello boy')
	}
}
object.sayHello() // hello boy
```

!> 属性名表达式与简洁表示法，不能同时使用，否则会报错。

```js
// 报错 
const name = 'alice'
const object = {
	[name]
}
// Uncaught SyntaxError: Unexpected token '}'

// 正确
const name = 'alice'
const object = {
	[name]: 'alice'
}
// {alice: "alice"}
```

---

### 拓展运算符

​	拓展运算符**`...`**可用于取出参数对象的所有可遍历属性，并将其拷贝到当前对象之中，这等同于**`Object.assign()`**。

```javascript
let x = {a: 3, b: 4}
let y = {...x}

y // {a: 3, b: 4}

let aClone = {...a}
// 等同于
let aClone = Object.assign({}, a)

// 拓展运算符可以实现对数组的复制
let arr = [1, 2, 3]
let arr2 = [...arr]
console.log(
	arr2, // [1, 2, 3]
	arr2 === arr // false
)

// 还可以用于展开数组或类数组
let box = [...document.getElementByClassName('box')]
```

​	

