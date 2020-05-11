# 严格模式拓展

​	从es5开始，函数内部可以设定为严格模式。只是在ES2016做了一点修改，规定只要函数参数使用了默认值、解构赋值、或者拓展运算符，那么函数内部就不能显示设定为严格模式，否则会报错。

```javascript
function fn(x = 1) {
	'use strict'
}
// Uncaught SyntaxError: Illegal 'use strict' directive in function with non-simple parameter list
```

