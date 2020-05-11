# 字符串模板

### 模板字符串

​	在 es6 中，为了使字符串的拼接更加简洁、直观，引入了**`模板字符串`**，字符串由**`  `` `**包裹，变量通过**`${}`**拼接。

```javascript
var first = '王'
var last = '小可'

// es5
var name = 'Your name is' + ' ' + first + last + '.' // Your name is 王小可.

// es6
var name = `Your name is ${first}${last}.` // Your name is 王小可.
```

---

### 标签模板

​	模板字符串可以紧跟在一个函数名后面，该函数将被调用来处理这个模板字符串，这被称为**`标签模板`**功能。

```javascript
alert `123`

// 等同于
alert(123)
```

!> 如果模板字符串里边有变量，就不是简单的调用了，而是会将模板字符串先处理为多个参数，再调用函数。

