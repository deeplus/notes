# Math拓展

​	es6 在**`Math`**对象上新增了17个与数学相关的方法，这些方法都是静态的，只能在**`Math`**对象上调用。

### Math.trunc()

​	去除一个数字的小数部分，返回整数部分。

​	不像 `Math` 的其他三个方法：**`Math.floor()`**、**`Math.ceil()`**、**`Math.round()`**，

​	**`Math.trunc()`** 的执行逻辑很简单，仅仅是**`删除`**掉数字的小数部分和小数点，不管参数是正数还是负数。

​	**`该方法传入的参数会被隐式转换为数字类型`**：对于非数值，**`Math.trunc()`**内部会使用**`Number()`**方法将其转为数值，对于空值和无法截取整数的值，返回**`NaN`**。

> 语法：**`Math.trunc(value)`**

```javascript
Math.trunc(0) // 0
Math.trunc(0.12) // 0
Math.trunc(-0.12) // -0

Math.trunc('0.12') // 0
Math.trunc('') // 0
Math.trunc(' ') // 0

Math.trunc(NaN) // NaN
Math.trunc('foo') // NaN
Math.trunc() // NaN
```

---

### Math.sign()

​	用于判断一个数是正数、负数、还是零。对于非数值，会将其先转换为数值，它总共会返回5种值：

* 参数为正数：返回**`1`**；
* 参数为负数：返回**`-1`**;
* 参数为0：返回**`0`**；
* 参数为-0：返回**`-0`**；
* 其他值：**`NaN`**。

​       该函数传入的参数会被**`隐式转换`**为数字。

> 语法：**`Math.sign(x)`**
>
> x : 任意数字

```javascript
Math.sign(2) // 1
Math.sign(-2) // -1
Math.sign(0) // 0
Math.sign(-0) // -0

Math.sign('-2') // -1
Math.sign(NaN) // NaN
Math.sign('foo') // NaN
Math.sign() // NaN
```

---

### Math.cbrt()

​	用于计算任意数字的立方根，对于非数值，**`Math.cbrt()`**内部也是先使用**`Number`**将其转为数值。

> 语法：**`Math.cbrt(x)`**

```javascript
Math.cbrt(1) // 1
Math.cbrt(-1) // -1
Math.cbrt(0) // 0
Math.cbrt(-0) // -0
Math.cbrt(Infinity) // Infinity
Math.cbrt(-Infinity) // -infinity
Math.cbrt(NaN) // NaN
Math.cbrt(null) // 0
Math.cbrt(undefined) // NaN
Math.cbrt(2) // 1.2599210498948732
```

```js
/* Polyfill */
if (!Math.cbrt) {
	Math.cbrt = function(x) {
		var y = Math.pow(Math.abs(x), 1/3)
		return x < 0 ? -y : y 
	}
}
```

---

### Math.hypot()

​	返回所有参数的平方和的平方根，如果有参数不能转换为数字，则返回**`NaN`**。

> 语法：**`Math.hypot(value1[, value2, ...])`**

```javascript
Math.hypot(3, 4) // 5
Math.hypot(3, 4, 5) // 7.0710678118654755
Math.hypot() // 0
Math.hypot(NaN) // NaN
Math.hypot(3, 4, 'foo') // NaN, +'foo' => NaN
Math.hypot(3, 4, '5') // 7.0710678118654755, +'5' => 5
Math.hypot(-3) // 3,the same as Math.abs(-3)
```

