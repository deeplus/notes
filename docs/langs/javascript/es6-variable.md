# 变量声明

### let

​	**`let`**声明的**`全局变量`**不会成为windows的属性，并且可以在不同的全局环境之间使用该变量。

```javascript
// 使用let不能重复声明变量
let a = 1
console.log(a) // 1
let a = 2
console.log(a) // SyntaxError: Identifier 'a' has already been declared
```

```html
<script src="01.js" defer></script>
<script src="02.js"></script>
```

```js
// 01.js
console.log(a) // 1
```

```js
// 02.js
let a = 1
```

---

### const

​		**`const`**声明的**`全局变量`**不会成为windows的属性，const用于声明**`常量`**，不能使用等号二次赋值。

```javascript
// 声明常量
const a = 1
console.log(a) // 1
a = 2
console.log(a) // Uncaught TypeError: Assignment to constant variable

// 用途：
const box = document.getElementById('box')
box.innerHTML = 123
box.style.colr = "blue"

// 当某一次出现误操作，修改了box
box = 1 // --> 直接报错
```
