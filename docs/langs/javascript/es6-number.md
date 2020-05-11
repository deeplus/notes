# Number拓展

​	es6 在**`Number`**对象上，新提供了**`Number.isFinite()`**和**`Number.isNaN()`**两个方法。

### Number.isFinite()

​	用来检测传入的参数是否是一个有穷数（finite number）。

> 语法：
>
> ```css
> Number.isFinite(value)
> ```
>

​		和全局的**`isFinite()`**函数相比，这个方法不会强制将一个非数值的参数转换成数值，这就意味着，只有数值类型的值，且是有穷的（finite），才返回 **`true`**。

```javascript
Number.isFinite(Infinity) // false
Number.isFinite(-Infinity) // false
Number.isFinite(NaN) // false

Number.isFinite(0) // true
Number.isFinite(2e64) // true, 2e64是4G个4G
Number.isFinite(Math.PI) // true

Number.isFinite('foo') // false
Number.isFinite('0') // false, 全局函数isFinite('0')会返回true
```

```js
/* Polyfill */

Number.isFinite = Number.isFinite || function(value) {
	return (typeof value === 'number') && isFinite(value)
}
```

---

### Number.isNaN()

​	确定传递的值是否为**`NaN`**和其类型是 **`Number`**。它是原始的全局**`isNaN()`**的更强大的版本。

> 语法：
>
> ```css
> Number.isNaN(value)
> ```
>
> 

​		和全局函数**`isNaN()`**相比，该方法不会强制将参数转换成数字，只有在参数是真正的数字类型，且值为 `NaN` 的时候才会返回**`true`**。

```javascript
Number.isNaN(NaN) // true
Number.isNaN(Number.NaN) // true
Number.isNaN(0 / 0) // true

// 下面这几个如果使用全局的 isNaN()时，会返回true
Number.isNaN('NaN') // false
Number.isNaN(undefined) // false
Number.isNaN({}) // false
Number.isNaN('blabla') // false

// 下面的都返回false
Number.isNaN(true) // false
Number.isNaN(null) // false
Number.isNaN(25) // false
Number.isNaN('25') // false
Number.isNaN('') // false
Number.isNaN(' ') // false
```

```js
/* Polyfill */

Number.isNaN = Number.isNaN || function(value) {
	return (typeof value === 'number') && isNaN(value)
}
```

---

​	es6 将全局方法**`parseInt()`**和**`parseFloat()`**移植到**`Number`**对象上面，行为完全保持不变。

​	这样做的目的是：逐步减少全局性方法，使得语言逐步**`模块化`**。

### Number.parseInt()

​	依据指定基数 [ 参数 **radix** 的值]，把字符串 [ 参数 **string** 的值] 解析成整数。

> 语法：
>
> ```css
> Number.parsseInt(string[, radix])
> ```
>
> 参数：
>
> * **`string`** ：要解析的值。 如果此参数不是字符串，则使用ToString抽象操作将其转换为字符串。忽略此参数中的前导空格。
>
> * **`radix`** ：一个介于2到36之间的整数，代表字符串的基数(数学数字系统中的基)。小心-这并不是默认为10。
>
> 

```javascript
Number.parseInt === parseInt // true

// es5的写法
parseInt(12.34) // 12

// es6的写法
Number.parseInt(12.34) // 12
```

```js
/* Polyfill */

if (Number.parseInt === undefined) {
	Number.parseInt = window.parseInt
}
```

---

### Number.parseFloat()

​	可以把一个字符串解析成浮点数，如果无法被解析成浮点数，则返回**`NaN`**

> 语法：
>
> ```css
> Number.parseFloat(string)
> ```
>

```javascript
Number.parseFloat = parseFloat // true

// es5写法
parseFloat('123.45#') // 123.45

// es6写法
Number.parseFloat('123.45#') // 123.45
```

---

### Number.isInteger()

​		用来判断传入的参数值是否为**`整数`**。需要注意的是：在JavaScript内部，整数和浮点数都是同样的储存方法，所以 3 和 3.0 被视为同一个值。

> 语法：
>
> ```css
> Number.isInteger(value)
> ```
>

```javascript
Number.isInteger(3) // true
Number.isInteger(3.0) // true
Number.isInteger(3.1) // false
Number.isInteger('3') // false

Number.isInteger(NaN) // false
Number.isInteger(Infinity) // false
Number.isInteger(true) // false
```
