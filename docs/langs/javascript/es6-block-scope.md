# 块作用域

​	es6 在 es5 的基础上新增了一个块级作用域，即**`{}`**.**`ES5声明变量的关键字只认全局和函数,ES6声明变量的关键字会去认{}`**，所以块作用域必须使用let声明。

```javascript
// es5声明变量的关键字只认全局和函数

if (true) {
	var a = 1 // 这是一个全局变量a
}
console.log(a) // 1 


// es6声明变量的关键字会去认{}
if (true) {
	let a = 1 // 这是一个局部变量a
	console.log(a) // 1
}
console.log(a) // ReferenceError: a is not defined


// 在es6中使用{}开辟一个块级作用域
{
	let a = 123
	console.log(a) // 123
}
console.log(a) // ReferenceError: a is not defined
```

