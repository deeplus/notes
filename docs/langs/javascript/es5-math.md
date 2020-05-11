# Math对象

​	Math是一个**`内置对象`**，它具有数学常数和函数的属性和方法，但它不是一个函数对象。

​	与其他全局对象不同的是，**`Math`** 不是一个构造器。 **`Math`** 的所有属性与方法都是静态的。引用圆周率的写法是 **`Math.PI`**，调用正余弦函数的写法是 **`Math.sin(x)`**，**`x`** 是要传入的参数。**`Math`** 的常量是使用 JavaScript 中的全精度浮点数来定义的。

### 属性

#### Math.E

​	欧拉常数，**`自然对数(loge，即ln)`**的底数，约等于2.718。

```javascript
// Math.E表示欧拉常数
var e = Math.E
console.log(e) // 2.718281828459045
```

---

#### Math.LN2

​	2的自然对数，约等于0.693。

```javascript
// Math.LN2表示2的自然对数
var ln2 = Math.LN2
console.log(ln2) // 0.6931471805599453
```

---

#### Math.LN10

​	10的自然对数，约等于2.303。

```javascript
// Math.LN10表示10的自然对数
var ln10 = Math.LN10
console.log(ln10) // 2.302585092994046
```

---

#### Math.LOG2E

​	以2为底E的对数，约等于1.443。

```javascript
// Math.LOG2E表示以2为底E的对数
var log2e = Math.LOG2E
console.log(log2e) // 1.4426950408889634
```

---

#### Math.LOG10E

​	以10为底E的对数，约等于0.434。

```javascript
// Math.LOG10E表示以10为底E的对数
var log10e = Math.LOG10E
console.log(log10e) // 0.4342944819032518
```

---

#### Math.PI

​	圆周率，约等于3.14159。

```javascript
// Math.PI表示圆周率
var pi = Math.PI
console.log(pi) // 3.141592653589793
```

---

#### Math.SQRT1_2

​	1/2的平方根，约等于0.707。

```javascript
// Math.SQRT1_2表示1/2的平方根
var g2 = Math.SQRT1_2
console.log(g2) // 0.7071067811865476
```

---

#### Math.SQRT2

​	2的平方根，约等于1.414。

```javascript
// Math.SQRT2表示2的平方根
var g2 = Math.SQRT2
console.log(g2) // 1.4142135623730951
```

---

### 方法

#### Math.abs(x)

​	返回x的绝对值。

```javascript
// Math.abs(x)返回x的绝对值
Math.abs(-1) // 1
```

---

#### Math.ceil(x)

​	**`向上取整`**，返回一个大于或等于给定数字的最小整数。

```javascript
Math.ceil(.95) // 1
Math.ceil(3) // 3
Math.ceil(4.001) // 5
Math.ceil(-2.313) // -2
```

---

#### Math.floor(x)

​	**`向下取整`**，返回一个小于或等于给定数字的最大整数。

```javascript
Math.floor(.95) // 0
Math.floor(3) // 3
Math.floor(4.001) // 4
Math.floor(-2.313) // -3
```

---

#### Math.round(x)

​	**`四舍五入`**，返回x四舍五入后最接近的整数。

```javascript
Math.round(.95) // 1
Math.round(4.501) // 5
Math.round(-5.449) // -5
```

---

#### Math.max(x, y, ...z)

​	**`最大值`**，返回一组数中的最大值。

```javascript
Math.max(-2, 5, 8, 10, 60) // 60
```

---

#### Math.min(x)

​	**`最小值`**，返回一组数中的最小值。

```javascript
Math.min(-2, 5, 8, 10, 60) // -2
```

---

#### Math.pow(x, y)

​	**`幂`**，返回x的y次幂。

```javascript
// es5
Math.pow(2, 3) // 8

// es6
2 ** 3 // 8
```

---

#### Math.sqrt(x)

​	**`平方根`**，返回x的平方根。

```javascript
Math.sqrt(4) // 2
```

---

#### Math.random(x)

​	**`随机数`**，返回一个**`[0, 1)`**之间的**`浮点数`**。

```javascript
// [0, 1)
Math.random()

// [0, 6)
Math.random() * 6

// [4, 35)
Math.random() * (35 - 4) + 4

// 得到一个两个数之间的随机整数，包括两个数在内
function getRandomIntInclusive(min, max) {
	min = Math.ceil(min);
	max = Math.floor(max);
	return Math.floor(Math.random() * (max - min + 1)) + min; //含最大值，含最小值 
}
```

---

### 三角函数

#### Math.sin(x)

​	返回x的正弦值（单位为弧度）。

```javascript
// 30度的正弦值
Math.sin(30 * Math.PI/180) // 0.49999999999999994
```

---

#### Math.cos(x)

​	返回x的余弦值（单位为弧度）。

```javascript
// 30度的余弦值
Math.cos(30 * Math.PI/180) // 0.8660254037844387
```

---

#### Math.tan(x)

​		返回x的正切值（单位为弧度）。

```javascript
// 30度的正切值
Math.tan(30 * Math.PI/180) // 0.5773502691896257
```

---

### 反三角函数

#### Math.asin(x)

​	返回x的反正弦值。

```javascript
// 30度的反正弦值
Math.asin(30 * Math.PI/180) // 0.5510695830994463
```

---

#### Math.acos(x)

​	返回x的反余弦值。

```javascript
// 30度的反余弦值
Math.acos(30 * Math.PI/180) // 1.0197267436954502
```

---

#### Math.atan(x)

​	返回x的反正切值。

```javascript
// 30度的反正切值
Math.atan(30 * Math.PI/180) // 0.48234790710102493
```

---

### 弧度/角度

#### 角度转弧度

> **`π/180 × 角度`**

```javascript
1 deg = (π / 180) rad
```

---

#### 弧度转角度

> **`180/π × 弧度`**

```javascript
1 rad = (180 / π) deg
```

