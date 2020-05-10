# 流程控制

### 六个假值

​		在JavaScript中，只有以下六个值在进行条件判断的时候会被转为 **`false`** ，其他都为 **`true`** ，这六个值分别为：**`""`** 、**`0`** 、**`NaN`** 、**`false`** 、**`undefined`** 、**`null`**

```js
var a = 2
if (a) {
	console.log('a为真值')
} else {
	console.log('a为假值')
}
// a为真值
```

!> **`NaN`** 是一个特殊的 **`数字`** ，表示一个 **`坏值`** ，其值不等于它本身。出现 **`NaN`** 一定是因为 **`进行了非法的数学运算`**

```js
// NaN值不等于其本身
NaN === NaN // false

// 出现NaN是因为进行了非法的数学运算
let a = 123
let b = 'a'
let c = a / b // NaN 
```

---

### if...else

当指定条件为真，**`if 语句`** 会执行一段语句。如果条件为假，则执行另一段语句。

> 语法：
>
> ```javascript
> if (condition)
> statement1
> [else
> statement2]
> ```
>
> 参数：
>
> * **`condition`**：值为真或假的**`表达式`**；
> * **`statement1`**：condition为真时执行的语句；
> * **`statement2`**：condition为假且**`else从句`**存在时执行的语句；
>

```javascript
// 使用if判断
var a = 3
if (a === 1) {
	console.log('a等于1')
} else if (a === 2) {
	console.log('a等于2')
} else if (a === 3) {
	console.log('a等于3')
} else {
	console.log('a不等于1、2、3其中一个')
}
```

---

### switch

​		**`switch`** 语句评估一个 **`表达式`**，将表达式的值与 **`case`** 子句匹配，并执行与该情况相关联的 **`语句`**。

​		如果在进行 **`if`** 判断时需要进行 **`多个分支`** 的确定，并且每个分支都是进行 **`===`** 判断时，可以使用**`switch`**。

> 语法：
>
> ```javascript
> switch (expression) {
> 	case value1:
> 		// 当expression的结果与value1匹配时，执行该处的代码
> 		break;
> 
> 	case value2：
> 		// 当expression的结果与value2匹配时，执行该处的代码
> 		break;
> 	
> 	default:
> 		// 当expression的结果与上面的value值都不匹配时，执行该处的代码
> 		break; // 该处的break可以省略，建议写上
> }
> ```

```javascript
// 上面的代码可以改写为下

var a = 3
switch (a) {
	case 1:
		console.log('a等于1')
		break;
	case 2:
		console.log('a等于2')
		break;
	case 3:
		console.log('a等于3')
		break;
	default:
		console.log('a不等于1、2、3其中一个')
		break;
}
```

---

### 三目运算

​		如果 **`if`** 判断 **`有且只有真假两个分支`** ，并且 **`每个分支只有一条语句`** ，就可以使用 **`三目运算`** 。

> 语法：
>
> ```javascript
> condition ? true branch : false branch;
> ```

```javascript
if (a > 4) {
	console.log('a大于4')
} else {
	console.log('a小于等于4')
}

// 上面的代码改写为三目
a > 4 ? console.log('a大于4') : console.log('a小于等于4');

// 也可以改写成
console.log(a > 4 ? 'a大于4' : 'a小于等于4')
```

