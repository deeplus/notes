# 迭代

### for

> 语法：
>
> ```javascript
> // for循环 -- 写法一
> for (初始值 ①; 判断条件 ②; 步幅 ③) {
> 	code ④;
> }
> 
> // for循环 -- 写法二
> 初始值 ①;
> for ( ;判断条件 ②; ) {
> 	code ④;
> 	步幅 ③;
> }
> 
> // 执行顺序为： ① -> ② -> ④ -> ③ -> ② -> ④ -> ③ -> ②
> ```

```javascript
// div标签绑定点击事件
var divs = document.getElementByClassName('box')

// 使用 var 声明
for (var i = 0; i < divs.length; i++) {
	div[i].idx = i // 使用自定义属性保存当前的i值
	div[i].onclick = function() {
		console.log(`当前点击的div的序号为：${this.idx + 1}`) // 通过this.idx访问当前的值
	}
}

```

```javascript
// 使用 let 声明
for (let i = 0; i < divs.length; i++) {
	div[i].onclick = function() {
		console.log(`当前点击的div的序号为：${i + 1}`)
	}
}
```

```javascript
// 使用闭包
for (var i = 0; i < divs.length; i++) {
	(function() {
		div[i].onclick = function() {
			console.log(`当前点击的div序号为：${i + 1}`)
		}
	}())
}
```

---

### while

> 语法：
>
> ```javascript
> // while循环
> 初始值 ①;
> while (判断条件 ②) {
> 	code ④;
> 	步幅 ③;
> }
> 
> // 执行顺序：
> ```

---

### do...while

> 语法：
>
> ```javascript
> // do while循环
> do {
> 	
> } while (判断条件)
> ```

---

### for...in

**`for...in`**语句以任意顺序遍历一个JSON格式对象的除**`Symbol`**以外的**`可枚举`**属性名。

> 语法：
>
> ```javascript
> for (key in object) {
> 	statements
> }
> ```

```javascript
var obj = {
	a: 1,
	b: 2,
	c: 3
}

for (var key in obj) {
	console.log(key)
}

// 'a'
// 'b'
// 'c'
```

---

### for...of

**`for...of`**语句用于遍历一个**`可迭代对象`**（array，set，map，string，类数组，arguments对象等）的属性值。

> 语法：
>
> ```javascript
> for (value of iterable) {
> 	statements
> }
> ```

```javascript
let arr = [10, 15, 20, 25]

for (var value of arr) {
	value += 5
	console.log(value)
}

// 15
// 10
// 25
// 30
```

