# 操作符

### .

​		每一个对象，系统自带的属性叫做`合法对象属性`，比如：`arr.length`；而人为定义的属性，叫做`非法对象属性`，即`自定义属性`，自定义属性存在于JavaScript环境中。

​		通过 **`.`** 标识符能够访问或设置`对象的属性`，但是在获取dom对象的`style`属性时，该操作符获取的是`行内样式`，如果获取不到则返回 **`""`**。

```js
// 获取一个dom对象属性
var element = document.getElementById('box')

element.id // 获取element元素的id
element.style // 获取element元素的行内样式

// 自定义属性
var alice = {}
alice.name = '小姣'
alice.age = 22
alice.sex = '女'
```

---

### []

​		`[]` 标识符作为 `.` 标识符符的替代品，弥补了 `.` 操作符之后不能是 `数字`、`变量` 的缺陷。

​		`[]` 标识符里边如果是变量，该变量如果未定义，那么会报错。		

```js
// 获取对象的属性
var obj = {
	a: 1,
	b: 2
}
var a = 'b'
obj['a'] // 1
obj[a] // 2, 变量a有定义，其值为'b',此时相当于obj['b']
obj[b] // b is not defined，变量b未定义，报错

// 获取数组指定index的值
var arr = [1, 2, 3, 4]
arr[0] // 1
```

!> 通过**`.`**操作符或**`[]`**操作符去访问一个对象不存在的属性时，返回**`undefined`**；

```js
var obj = {
	a: 1
}
obj.b // undefined
obj['c'] // undefined
```

---

### typora

​		`typeof` 操作符返回一个字符串，表示未经计算的操作数的类型。

> 语法：typeof后接操作数。
>
> ```js
> typeof operand
> 
> // 也可以写成
> typeof(operand)
> ```
>
> 参数：
>
> * `operand`：一个表示对象或原始值的表达式，其类型将被返回。
>
> 

```js
typeof 123 // 'number'
typeof(123) // 'number'
```



!> `typeof` 运算符在判断数据类型时，存在两个特殊情况：

* **`typeof null`** 返回的是**`object`**而不是null

```js
var nul = null
typeof nul // object
```



* **`typeof function`**返回的是**`function`**而不是object

```js
var fn = function(){}
typeof fn // function
```



---

### instanceof

​			通过**`instanceof`**二元运算符也可以对对象的类型进行判断，其原理就是测试构造函数的**`prototype`**是否出现在被检测对象的原型之上。该方法用于判断一个对象是否存在于另一个对象的**`原型链`**上。

> 语法：
>
> ```javascript
> object instanceof constructor
> ```
>
> 参数：
>
> * **`object`**：某个实例对象；
> * **`constructor`**：某个构造函数
>

!> **`instanceof`** 运算符用来检测 **`constructor.prototype`**是否存在于参数 **`object`**的原型链上。

```javascript
function Fn1() {}
function Fn2() {}

var fn1 = new Fn1()

fn1 instanceof Fn1 // true
fn1 instanceof Fn2 // false
fn1 instanceof Object // true
fn1 instanceof Function // false
```

---

### in

**`in`**运算符用于检测某个属性是否存在于指定的对象或其原型链中，返回一个布尔值。

> 语法：
>
> ```javascript
> prop in object
> ```
>
> 参数：
>
> * **`prop`**：一个字符串类或者symbol类型的属性名或者数组索引（非symbol类型将会强制转为字符串）。
>
> 

```javascript
// in用于判断某个属性是否存在于指定对象或其原型链上
var obj = {
	a: 1,
	b: 2,
	c: 3
}

'a' in obj // true
```

---

### delete

**`delete`**操作符用于删除对象的某个属性，返回一个布尔值。

> 语法：
>
> ```javascript
> delete expression
> 
> // expression 的 计算结果应该是某个属性的引用，所以可以改写为：
> delete object.property
> 
> // 或者
> delete object['property']
> ```
>
> 参数：
>
> * **`object`**：对象的名称;
> * **`property`**：要删除的属性。
>

```javascript
// delete用于删除对象的属性
var obj = {
	a: 123
}
delete obj.a
console.log(obj.a) // undefined
```



​		**`delete`**能够删除泄露的变量，但是**`不能删除关键字声明的变量`**。

```javascript
var a = 123
b = 456

delete a
delete b

console.log(a) // 123
console.log(b) // b is not defined
```

---

### new

​		**`new`**运算符创建一个用户定义的对象类型的实例或具有构造函数的内置对象的实例。构造函数被**`new`**执行的过程叫做**`类的实例化`**。

​		**`new`**关键字会进行如下操作：

* **`new`**执行的函数，函数内部默认生成一个对象；
* 函数内部的**`this`**默认指向这个**`new`**生成的对象；
* **`new`**执行函数生成的这个对象，是函数的默认返回值。

```javascript
function fn() {
    console.log(this)
}
new fn() // fn {}
```



---

### super

​		**`super`**关键字用于访问和调用一个对象的父对象上的函数。在构造函数中使用时，**`super`**关键字将单独出现，并且必须在使用**`this`**关键字之前使用。

> 语法：
>
> ```javascript
> // 调用 父对象/父类 的构造函数
> super([arguments])
> 
> // 调用 父对象/父类 上的方法
> super.functionOnParent([arguments])
> ```

```javascript
// 父类
class Father {
    constructor(opt) {
        this.name = opt.name
    }
    
    sayName() {
        console.log("hello, I'm " + this.name)
    }
}

// 子类
class Son extends Father {
    constructor(opt) {
        super(opt) // 必须调用且必须使用在this之前调用
        this.age = opt.age
    }
    
    sayAge() {
        console.log("hello, I'm " + this.age)
    }
}
```



