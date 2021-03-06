# 作用域

​	**`作用域`**：即变量生效的环境，在es5中作用域有两类，分别是**`全局作用域`**和**`函数作用域`**。

​	**`作用域链`**：由不同作用域之间形成的**`相互嵌套关系`**，被称为**`作用域链`**。

### 全局作用域

​	在 Javascript 中，最大的作用域被称为**`全局作用域`**，它是全局代码的执行环境。每一个 script 标签就是一个全局作用域，但是顶层对象只有一个。

```javascript
// 每一个script标签就是一个全局作用域

// 这是一个全局作用域
  
var a = 1 // 这是一个全局变量
```

---

### 函数作用域

​	在 JavaScript 中，每一个函数执行都会开辟一个新的作用域，即**`函数作用域`**。

```javascript
var a = 1 // 这是全局变量

function fn() {
	// 每一个函数，都会开辟一个新的函数作用域
}
```

---

### 作用域雷区

#### 变量泄露

​	无论在何种作用域下，如果一个变量没有声明就直接赋值，那么该变量就有可能**`泄露`**成为**`顶层对象(window)`**的属性，就可以在任何作用域访问到该变量。但是需要注意，顶层对象的属性不是全局变量。

​	在全局环境中，一个变量未声明就赋值，该变量会**`直接泄露`**成为顶层对象的属性。

```js
// 全局环境
a = 1 // 未声明就赋值，变量直接泄露

function fn () {
	console.log(a)
}
fn() // 1
console.log(a) // 1
console.log(window.a) // 1
```

在函数作用域中，如果一个变量未声明就赋值，该变量**`不一定`**会泄露，必须等到**`函数作用域被激活`**才会泄露。

```js
// 函数作用域
function fn () {
	a = 1
	console.log(a)
}
console.log(window.a) // ReferenceError: a is not defined
fn() //1， 函数作用域被激活，变量才会泄露
console.log(a) // 1
console.log(window.a) // 1
```

---

#### 属性挂载

​	**`var`**和**`function`**声明的**`全局变量`**也会自动成为**`window对象的属性`**，同样会污染顶层对象的属性环境。

```javascript
var a = 123
console.log(window.a) // 123 var声明的全局变量会被挂载到window下面

function b() {
	// function声明的全局变量同样会被挂载到window下面
}
console.log(window.b) // ƒ b(){}
```

---

#### 作用域链

​	由于变量的查找是沿着作用域链来实现的，因此作用域链也被成为**`变量查找的机制`**。即内部环境可以通过作用域链访问所有外部环境，但外部环境不能访问内部环境的任何变量和函数，该机制也说明了访问局部变量要比访问全局变量更快。

```javascript
// 内部环境可以访问所有的外部环境
var a = 123
function fn() {
	console.log(a) 
}
fn() // 123
console.log(a) // 123

// 外部环境不能访问内部环境
function fn() {
	var a = 123
	console.log(a)
}
fn() // 123
console.log(a) // ReferenceError: a is not defined
```

---

### 函数作用域误区

​	函数作用域在什么地方不是看函数是在哪里调用，而是看函数是在哪里定义。函数一旦被定义，作用域就已经存在，只是该作用域需要在函数调用的时候才会被激活。

```javascript
// 1
var a = 3
function fn() {
	// 2
}
function fn2() {
	// 3
	var a = 2
	fn() // 作用域2被激活
}
fn2() // 3 作用域3被激活 
// 三个作用域的关系为：1 > 2、3
```

