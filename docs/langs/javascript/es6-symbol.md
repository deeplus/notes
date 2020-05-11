# Symbol

### Symbol是什么

​	**`Symbol`**实际上是es6引入的一种原始数据类型。除了symbol，JavaScript还有其它5种基础类型和1种复杂类型，分别是：undefined、null、boolean、string、number和object。

> 语法：
>
> **`Symbol([description])`**
>
> * **`desciption`**：可选，字符串类型，是对symbol的描述，可用于调试但不是访问symbol本身。

```javascript
var sym = Symbol()
var sym1 = Symbol('foo')
var sym2 = Symbol(123)

sym // Symbol()
sym1 // Symbol(foo)
sym2 // Symbol(123)
```

---

### 为什么需要Symbol

​	es5里面对象的属性名都是字符串，如果你需要使用一个别人提供的对象，你对这个对象有哪些属性也不是很清楚，但又想为这个对象新增一些属性，那么你新增的属性名就很有可能和原来的属性名发生冲突，显然我们是不希望这种情况发生的。所以我们要确保每个属性名是独一无二的，这样就可以防止属性名冲突。因此，es6就引入了symbol，用它来产生一个独一无二的值。

---

### 如何产生一个Symbol

​	symbol是一种原始数据类型，它的值是通过symbol函数生成的。需要注意的是：**`Symbol函数不是一个构造函数`**，前面不能用new操作符，所以symbol类型的值也不是一个对象，不能添加任何属性。它只是一个类似于字符型的数据类型，如果强行在Symbol函数前加上new操作符，会报错。

```javascript
var sym1 = Symbol('foo')
typeof sym1 // symbol

var sym2 = new Symbol('foo') // Symbol is not a constructor
```

---

### Symbol的参数

#### 字符串作为参数

​	Symbol函数可以接收一个字符串参数，来对产生的Symbol值进行描述，方便我们区分不同的Symbol值。

* 给Symbol函数加了参数之后，控制台可以区分到底是哪一个Symbol值。
* Symbol函数的参数只是对当前Symbol值的描述，因此相同参数的Symbol函数返回值是不相等的。

```javascript
let s1 = Symbol('s1')
let s2 = Symbol('s2')
s1 === s2 // false

let s3 = Symbol('s2')
s2 === s3 // false
```

---

#### 对象作为参数

​	如果Symbol函数的参数是一个对象，就会调用该对象的toString方法，将其转为一个字符串，然后才生成一个Symbol值。所以，说到底Symbol函数的参数只能是字符串。

```javascript
let s = Symbol({})
s // Symbol([object Object])
```

---

### Symbol值不能进行运算

​	Symbol虽然是一种原始数据类型，但是symbol值不仅不能和symbol值进行运算，也不能和其它类型的值进行运算，否则会报错。

​		Symbol值可以显示转换为字符串和布尔值，但是不能转为数值。

```javascript
let sym1 = Symbol('my symbol1')

String(sym1) // 'Symbol(my symbol1)'
Boolean(sym1) // true

Number(sym1) //  Cannot convert a Symbol value to a number

let sym2 = Symbol('my symbol2')

sym1 + sym2 // Cannot convert a Symbol value to a number
```

---

### Symbol做属性名

​	Symbol就是为做对象的属性名而生，用Symbol做对象的属性名，有以下几种写法：

```javascript
let obj = {}
let propsym = Symbol()

// 写法1:
obj[propsym] = 'mySymbol'

// 写法2:
obj = {
	[propsym]: 'mySymbol'
}

// 写法3:
Object.defineProperty(obj, propsym, {value: 'mySymbol'})

// 取值
obj.propsym // undefined
obj[propsym] // 'mySymbol'
```

* 使用Symbol值作为对象的属性名时，获取相应的属性值不能用**`.`**运算符；
* 如果用**`.`**运算符来给对象的属性赋Symbol类型的值时，实际上属性名会变成一个字符串，而不是一个Symbol值；
* 在对象内部，使用Symbol值定义属性时，symbol值必须放在**`[]`**中，否则只是一个字符串。

---

### Symbol值做属性名的遍历

​	symbol值作为对象的属性名时，使用**`for...of`**和**`for...in`**无法遍历到symbol值的属性，也不能通过**`Object.keys()`**和**`Object.getOwnPropertyNames()`**获取到对象的属性名。但是不用担心，我们可以使用**`Object.getOwnPropertySymbols()`**获取一个对象上的Symbol属性名，也可以使用**`Reflect.ownKeys()`**返回所有类型的属性名，包括常规属性名和Symbol属性名。

​		利用symbol值作为对象的属性名时不会被常规的方法遍历到这一特性，可以为对象定义一些非私有但又只希望对象内部可用的方法。

```javascript
let s1 = Symbol('s1')
let s2 = Symbol('s2')
let a = {
	[s1]: 's1',
	[s2]: 's2',
	hello: 'hello'
}

Object.getOwnPropertySymbols(a) // [Symbol(s1), Symbol(s2)]
Reflect.ownKeys(a) //  ["hello", Symbol(s1), Symbol(s2)]
```

---

### 方法

#### Symbol.for()

​	接收一个字符串作为参数，然后搜索有没有以该参数作为描述的symbol值，如果有，就直接返回该symbol值；如果没有，则以该参数作为描述创建一个新的symbol值。

> 语法：
>
> ```js 
> Symbol.for(key)
> ```
>
> 参数：
>
> * **`key`**：一个字符串，作为 symbol 注册表中与某 symbol 关联的键（同时也会作为该 symbol 的描述）。

```js
let sym1 = Symbol('123')
let sym2 = Symbol.for('123')
console.log(sym1 === sym2) // false ---> Symbol()生成的symbol值没有登记机制
```

```javascript
// 没有以'123'为关联键的symbol值 ---> 创建以'123'为描述的symbol值
let sym1 = Symbol.for('123') // Symbol(123)

// 已经存在以'123'为关联键的symbol值 --> 返回
let sym2 = Symbol.for('123') // Symbol(123)

sym1 === sym2 // true
```

​	**`Symbol.for()`**函数可以用来生成一个symbol值，该函数有一个特殊的用处：**`可以重复使用一个symbol值`**。

---

#### Symbol.keyFor()

​	获取symbol注册表中与某个symbol关联的键，如果全局注册表中查找到该symbol，则返回该symbol的key值，形式为string；如果symbol未在注册表中，返回undefined。

​	**`Symbol.keyFor()`**是用来查找一个symbol值的登记信息的，但是**`Symbol()`**写法没有登记机制，所以在查找**`Symbol()`**函数生成的symbol关联的键时，返回undefined。而**`Symbol.for()`**函数会将生成的symbol值登记在全局环境中，所以可以查找到用**`Symbol.for()`**函数生成的symbol值。	

```javascript
var sym1 = Symbol('mySymbol1')
var sym2 = Symbol.for('mySymbol2')

Symbol.keyFor(sym1) // undefined
Symbol.keyFor(sym2) // 'mySymbol2'
```

