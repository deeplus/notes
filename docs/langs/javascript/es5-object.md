# Object对象

​	**`Object`**对象是位于原型链顶端的对象，几乎所有JavaScript中的对象都是它的实例。如果将一个方法拓展到**`Object.prototype`**上，就意味着JavaScript里的任何对象都能调用该方法。

```javascript
Object.prototype.smaile = function () {
	console.log(this) 
}

;(123).smaile() // Number {123}
true.smaile() // Boolean {true}
```

---

### 属性

​	JavaScript共有两种属性，一种**`数值属性`**，一种**`访问器属性`**。访问器属性不包含数值，而是包含一对**`getter`**和**`setter`**函数。

​	当读取访问器属性时，会调用**`getter`**函数并返回有效值；在写入访问器属性时，会调用**`setter`**函数并传入新值，将传入的数据进行处理。

#### getter

​	**`get`**语法将对象属性绑定到查询该属性时将被调用的函数。

> 语法：
>
> ```javascript
> { get prop() { /*...*/ } }
> 
> // 或者
> { get [expression]() { /*...*/ } }
> ```
>
> 参数：
>
> * **`prop`**：要绑定到给定函数的属性名，可以是数字或字符串，但是**`不能带参数`**。
> * **`expression`**：从 ECMAScript 2015 开始，还可以使用一个计算属性名的表达式绑定到给定的函数。

---

##### 对象初始化时定义getter

​	有时需要允许访问返回动态计算值的属性，或者你可能需要反映内部变量的状态，但又不希望通过显式方法调用，这时候你就可以通过**`getter`**来实现。

​	例如下面的代码：能够在obj对象初始化时创建一个伪属性 `latest` ,它会返回 `log`数组的最后一个值，

```javascript
var obj = {
	log: ['exaple', 'test'],
	get latest() {
		if (this.log.length === 0) return undefined
		return this.log[this.log.length - 1]
	}
}
```

​	es6允许使用一个计算属性名的表达式绑定到给定的函数。

```javascript
let expr = 'foo'
let obj = {
	get [expr]() {
		return 'bar'
	}
}

obj[expr] // 'bar'
obj.foo // 'bar'
```

---

##### 现有对象定义getter

​	为现有对象添加**`getter`**时，不能直接定义，必须使用**`Object.defineProperty()`**来定义。

```javascript
var obj = {
	a: 1
}
Object.defineProperty(obj, 'b', {
	get: function() {
		return this.a + 1
	}
})

obj.b // 2
```

---

##### 删除getter

​	通过**`delete`**操作符，就能删除**`getter`**。

```javascript
delete obj.latest
```

---

#### setter

​	当尝试设置属性时，**`set`**语法将对象属性绑定到要调用的函数。

> 语法：
>
> ```javascript
> { set prop(val) {/* ... */} }
> 
> // 或者
> { set [expression](val) {/* ... */} }
> ```

##### 对象初始化时定义setter

​	在 javascript 中，如果试着改变一个属性的值，那么对应的 **`setter`** 将被执行。**`setter`** 经常和 **`getter`** 连用以创建一个**`伪属性`**。不可能在具有真实值的属性上同时拥有一个 setter 器。

​	例如下面的代码：定义一个对象 language 的伪属性 current，当给 current 分配一个值时，使用该值更新log。

```javascript
var language = {
	set current(name){
		this.log.push(name)
	},
	log: []
}

language.current = 'alice'
language.log // ["alice"]

language.current = 'rabbit'
language.log // ["alice", "rabbit"]
```

es6允许使用一个计算属性名的表达式绑定到给定的函数。

```javascript
let expr = 'foo'

let obj = {
	baz: 'bar',
	set [expr](v) {
		this.baz = v
	}
}

obj.baz // 'bar'
obj.foo = 'baz'
obj.baz // 'baz'
```

---

##### 现有对象定义setter

```javascript
var obj = {
	a: 1
}

Object.defineProperty(obj, 'b', {
	set: function(x) {
		this.a = x
	}
})

obj.b = 10
obj.a // 10
```

---

##### 删除setter

```js
delete obj.current
```

---

#### this的指向

​	**`getter/setter`**绑定的函数，内部的**`this`**指向一个对象，除**`getter/setter`**绑定的函数之外，其它属性自动成为该对象的成员。

```js
// get 语句之前有属性
var obj = {
	a: 1,
	b: 2,
	get foo() {
		console.log(this)
	},
	c: [1, 2, 3]
}
obj.foo // {a: 1, b: 2, c: [1, 2, 3]}

// get 语句之前无属性
var obj = {
	get foo() {
		console.log(this)
	}
}
obj.foo // {}
```

---

### 方法

#### Object.create()

​	用于创建一个新对象，该方法会根据提供的对象来创建新对象的**`_proto_`**，并返回一个带着指定的原型对象和属性的新对象。

> 语法：
>
> ```css
> Object.create(proto[, propertiesObject])
> ```
>
> 参数：
>
> * **`proto`**：新创建对象的原型对象；
>
> * **`propertiesObject`**(可选)：要为新创建对象添加的属性及属性值，该参数的写法见**`Object.defineProperties()`**。
>

```javascript

```

---

#### Object.getPrototypeOf()

​	返回指定对象的原型（内部`[[Prototype]]`属性的值），如果没有继承属性，则返回null。

> 语法：
>
> ```css
> Object.getPrototypeOf(object)
> ```
>
> 参数：
>
> * **`object`**：要返回其原型的对象。
>

```javascript

```

---

#### hasOwnProperty()

​	用来检测一个对象是否具有某个属性，所有继承了**`Object`**的对象都会继承到 **`hasOwnProperty`**方法。这个方法可以用来检测一个对象是否含有特定的自身属性；和**`in`**运算符不同，该方法会忽略掉那些从原型链上继承到的属性。

> 语法：
>
> ```css
> obj.hasOwnProperty(prop)
> ```
>
> 参数：
>
> * **`prop`**：要检测的属性的**`String`**字符串形式表示的名称，或者 **`Symbol`**。
>

```javascript
function Person(name) {
	this.name = name
}
Person.prototype = {
	age: function () {}
}
var obj = new Person('alice')

// hasOwnProperty不会查找原型链
obj.hasOwnProperty('name') // true
obj.hasOwnProperty('age') // false

// in操作符会去查找原型链
'name' in obj // true
'age' in obj // true
```

---

### 包装对象

​	**`包装对象`**指的是数据类型为**`String`**、**`Number`**、**`Boolean`**的值对应的原生对象，包装对象的意义在于：

* 能够将基本类型值包装成真正的对象，从而体现**`JavaScript` **中一切皆对象的特点；

* 是字面量使用对应包装对象的方法的内在原理；

* 是进行数据类型转换的利器。

#### 字面量和包装对象的区别

​	基本数据类型可以通过字面量的形式创建，也可以通过对应的包装对象来创建，二者的区别在于一个是值类型数据，一个是引用型数据。

```javascript
var s1 = '123' // 值类型
var s2 = new String('123') // 引用型
```

---

#### 包装对象的原理

​	包装对象的原理：每次值类型字面量在调用包装对象实例的方法时，首先会创建一个对应包装对象的实例，然后在实例上调用该方法，最后销毁该实例，这也就是为什么值类型字面量能够调用包装对象的实例方法。

```javascript
var str = 'hello'
str.split(' ')

// 等价于
var str = new String('hello')
str.split(' ')
str = null
```

​		因此，对字面量属性进行赋值时都是无效的，因为每次字面量调用完包装对象实例的方法后都会销毁实例。

```javascript
var str = '123'
str.num = 1 // 进行str.num操作时，String包装对象创建了一个实例，该实例在操作完成之后被销毁
console.log(str.num) // undefined ，所以此处的进行str.num操作时创建了一个新的对象实例，相当于console.log(str.num = undefined)
```

---

#### 包装对象和Object的关系

​	**`Object`**是一切对象的构造函数，因此包装对象的实例是由**`Object`**来构造的。

```javascript
var num = new Object(1) // 等价于 new Number(1)
var str = new Object('hello') // 等价于 new String('hello')
var bool = new Object(true) // 等价于 new Boolean(true)
```

---

### 对象的拷贝

#### 深/浅拷贝

```js
/*
*	o1: 接收一个对象或数组
*	deep: true表示深拷贝，false表示浅拷贝
*/

function extend(o1, deep) {
	// o1为JSON对象
	var obj = {}
    
	// o1为数组对象
	if (o1 instanceof Array) { // 返回true，表明o1是一个数组
		obj = []
	}
    
	for (var key in o1) {
		var value = o1[key]
    
		// 如果deep为true,则表明需要进行深拷贝
		obj[key] = (!!deep && typeof value === 'object' && value !== 'null') ? extend(value, deep) : value;
		// !!deep ：强制将deep转为布尔值,不传值默认undefined,转为false，浅拷贝
		// typeof value === 'object' :传入的值如果是{}或[]，则需要深拷贝，否则就是浅拷贝，直接赋值即可
		// value !== 'null' ：需要排除null, 因为typeof null === 'object'
		// function不需要考虑
	}
	return obj
}
```

---

#### 不支持函数的深拷贝

```js
function extend(o1) {
	var str = JSON.stringify(o1)
	var obj = JSON.parse(str)
	return obj
}
```

