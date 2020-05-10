# 显示强制类型转换

### 对象转数字

​	**`Number()`**、**`parseInt()`**、**`parseFloat()`**三个方法都为显示强制类型转换。

#### Number()

​	JavaScript通过内建函数**`Number()`**能够将一个字符串转为数字，如果出现非法字符，就转为**`NaN`**。**`Number()`**将一个对象转换为数字的时候，会**`隐式调用`**该对象的**`toString()`**方法，先将该对象转换为一个字符串，再把对应字符串转换为数字。以下为特殊情况：

*    **`''`** 、**`' '`** 、**`null`** 、**`false`** 、**`[]`** 会被 **`Number()`** 转为 **`0`** ；
*    **`undefined`** 、**`{}`** 会被 **`Number()`** 转为 **`NaN`** ;
*    **`true`** 会被 **`Number()`** 转为 **`1`** ；
*    对于数组而言，如果为 **`单条数据且没有非法数字`** ，则转为对应数字，否则转为 **`NaN`** 。

```javascript
// 合法字符转为对应数字
Number('+123') // 123
Number('-123') // -123

// 出现非法字符，转为NaN
Number('abc') // NaN
Number('12a') // NaN

// ''、' '、null、false、[]会被转为0
Number('') // 0
Number(' ') // 0
Number(null) // 0
Number(false) // 0
Number([]) // 0

// undefined、{}会被转为NaN
Number(undefined) // NaN
Number({}) // NaN

// true会被转为1
Number(true) // 1

// 数组 -- 单条数据
Number([123]) // 123
Number(['123']) // 123

// 数组 -- 多条数据
Number([123, 456]) // NaN
Number([123, 'abc']) // NaN

// Number()方法会隐式调用对象的toString()方法,如果显示定义toString()的返回值，就可以影响运算结果
var obj = {
	toString: function(){
		return 123;
	}
}
Number(obj) // 123
```

---

#### parseInt()

​		JavaScript通过内建函数 **`parseInt()`** 能够将一个小数转为一个整数。其实现原理为：当传入一个参数时，会将该参数从左往右进行检查 **`(会忽略开始的空格字符)`** ，当遇到 **`非数字(+、-除外)`** 的时候就停止，再将前面的值作为返回值，如果不能转换，就返回 **`NaN`** ，该方法会 **`隐式调用toString()方法`** 。

```javascript
// 遇到非数字就停止
ParsetInt(12.56) // 12
Parseint('100px') // 100
parseInt('12a12') // 12

// +、-除外
parseInt(-12.56) // -12
parseInt('+120px') // 120

// 会忽略开始的空格字符
parseInt('    -123px') // -123

// 不会忽略中间的空格字符
parseInt('   -12 315') // -12

// 该方法会隐式调用toString()
parseInt([123, 'a', 2]) // 123,  [123, 'a', 2].toString() ---> "123,a,2"
parseInt(['a']) // NaN

parseInt(.12) // 0 , 	(.12).toString() --> "0.12"
parseInt('.12') //NaN,  ('.12').toString() --> ".12"
```

---

#### parseFloat()

   JavaScript通过内建函数**`parseFload()`**能够取到一个正常数字的浮点数，其 **`原理与parseInt()相似`** 。该方法也会 **`隐式调用toString()`** 。

```javascript
parseFloat(' -123.35456 87px') // -123.35456
parseFloat('') // NaN
parseFloat([]) // NaN
parseFloat([1]) // 1
```

---

### 对象转字符串

​	**`null`** 、**`undefined`** 能够被 **`String()`** 转为字符串，但是不能调用 **`toString()`** 方法。

#### String()

​	JavaScript通过内建函数 **`String()`** 能够将一个对象转换为字符串，该方法会 **`隐式调用toString()`** 。

```javascript
String(122) // '122'
String(null) // 'null'
String(undefined) // 'undefined'

// 该方法会调用toString()
var obj = {
	a: 1,
	b: 2,
	c: 3
}
String(obj) // '[object Object]'

// String()方法会隐式调用对象的toString()方法,如果显示定义toString()的返回值，就可以影响运算结果
let obj = {
	toString: function(){
		return "hello"
	}
}
String(obj) // 'hello'
```

---

#### toString()

​	JavaScript通过对象的 **`toString()`** 方法同样能够将一个对象转为字符串。

```javascript
// null和undefined不能调用toString()

(null).toString() // TypeError: Cannot read property 'toString' of null

(undefined).toString() // TypeError: Cannot read property 'toString' of undefined
```

---

### 对象转布尔值

#### Boolean()

​	JavaScript通过内建函数 **`Boolean()`** 能够将一个对象转为布尔值，在JavaScript中，只有 **`''`** 、**`0`** 、**`NaN`** 、**`false`** 、**`undefined`** 、**`null`** 会被转为 **`false`** ，其他全为 **`true`** 。

```javascript
Boolean('hello') // true
Boolean(1234567) // true
Boolean(0) // false
Boolean(1/'a') // false
```

