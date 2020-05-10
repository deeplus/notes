# IIFE

​	**`IIFE`**全称 Immediately Invoked Function Expression，即**`立即执行函数表达式`**。

​	JavaScript中几种必须写**`;`**的情况：**`()`**、**`[]`**开头。

### IIFE的六种写法

```js
// 01. IIFE写法一
;(function () {
	// code...
})()

// 02. IIFE写法二
;(function () {
	// code...
}())

// 03. IIFE写法三
!function () {
	// code...
}()

// 04. IIFE写法四
~function () {
	// code...
}()

// 05. IIFE写法五
+function () {
	// code...
}()

// 06. IIFE写法六
-function () {
	// code...
}()
```

---

### IIFE与函数表达式的区别

​	**`IIFE`**必须立即执行，而函数表达式可以通过名字调用。

```js
// 函数表达式可以加()自执行
var fn = function () {
	console.log(1)
}() // 1

// 亦可以通过函数名调用
var fn = function () {
	console.log(1)
}
fn() // 1

// 但是需要注意，函数表达式一旦加()自执行，就不能再通过函数名调用
var fn = function () {
	console.log(1)
}() // 1
fn() // TypeError: fn is not a function
```

---

### IIFE的意义

​	在 es6 之前没有块作用域的概念，而所有的全局环境是互通的，因此不同js文件之间的全局变量会相互干扰，**`IIFE`** 的作用就在于，能够开辟一块**`局部作用域`**，避免出现全局变量而相互干扰。

​	因此，可以将**`IIFE`**理解为是块作用域在 es5 时期的替代品。

```html
<script>
	// 开辟一块局部作用域
	;(function () {
		var a = 1
	})()
</script>

<script>
	// 开辟一块局部作用域
	;(function () {
		var a = 2
	})()
</script>

<!-- 上面两个环境中的var声明的a不会相互干扰 -->
```

