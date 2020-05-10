# 数据类型

​		JavaScript中共有五种**`基础`**数据类型：**`Number`**、**`String`**、**`Boolean`**、**`Undefined`**、**`Null`**和一种**`复合`**数据类型**`Object`**。

---

### Number

```js
// 原始类型 -- 数字
var num = 123
typeof num // number
```

---

### String

```js
// 原始类型 -- 字符串
var str = 'hello'
typeof str // string
```

---

### Boolean

```js
// 原始类型 -- 布尔值
var bool = true
typeof boo // boolean
```

---

### Undefined

​		**`JavaScript`**是弱类型语言，而且**`JavaScript`**声明变量的时候并没有预先确定的类型，变量的类型就是其值的类型，即**`变量的类型由它的值来决定`**。在开发的过程中，有时候可能会遇到这种情况：在后续开发中，会需要用到某个变量，但目前又不确定该变量的值类型，就可以**`先声明该变量而不赋值`**，一旦出现这种情况，**`JavaScript的解释器就会给该变量赋上一个undefined的值`**。

​		**`undefined`**表示**`一个变量声明的时候未被初始化值，是程序的默认初始化值`**，准确的来说是设计程序的时候出现失误，搞出来的一个bug。

```js
// 原始类型 -- undefined
var a; // JavaScript引擎： a = undefined
typeof a // undefined
```

---

### Null

​		**`typeof`**运算符在判断**`null`**的数据类型时，会返回**`object`**，这是JavaScript自带的bug。

​		**`null`**代表**`空对象指针`**，在其他语言里同样存在。

```js
// 原始类型 -- null
var unl == null
typeof nul // object
```

---

### Object

​		对象类型也叫引用类型，**`array`**和**`function`**是对象的子类型。对象在逻辑上是属性的无序集合，是存放各种值的容器。对象值存储的是引用地址，所以和基本类型值不可变的特性不同，对象值是可变的。

​		JavaScript作为一门**`函数式`**编程语言，函数在JavaScript中占有很大的比重，用途非常广泛，为了能够很直观的确定函数，JavaScript的作者就设计了**`typeof`**在判断函数的时候不返回**`object`**，直接返回**`function`**，所以**`typeof`**运算符在判断函数的数据类型时，返回的是**`function`**而不是object。

```js
// 复合类型 -- object，也叫引用类型

// json对象
var obj = {}
typeof obj // object

// 数组
var arr = []
typeof arr // object

// 函数
var fn = function(){}
typeof fn // function
```