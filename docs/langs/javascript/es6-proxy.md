# Proxy

​	**Proxy** 对象用于定义基本操作的自定义行为（如属性查找，赋值，枚举，函数调用等）。**`Proxy`**可以修改某些操作的默认行为，等同于在语言层面作出修改，所以属于一种**`元编程`**，即对编程语言进行编程。

​	**`Proxy`**可以理解成：在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先经过这层拦截，因此提供了一些机制，可以对外界的访问进行过滤和改写。**`Proxy`**这个词的原意是代理，用在这里表示由它来代理某些操作，可以译为“**`代理器`**”。

### 创建一个代理器对象

​		es6 原生提供 Proxy 构造函数，用来生成 Proxy 实例。

> 语法：
>
> **`let proxy = new Proxy(target, handler)`**
>
> 参数：
>
> * **`target`**：用`Proxy`包装的目标对象（可以是任何类型的对象，包括原生数组，函数，甚至另一个代理）。
> * **`handler`**：一个对象，其属性是当执行一个操作时定义代理的行为的函数。

```javascript
let proxy = new Proxy(target, handler)
```

​	Proxy对象的所有用法，都是上面这种形式，不同的只是**`handler`**参数的写法。其中，**`new Proxy()`**表示生成一个**`Proxy`**实例，**`target`**参数表示所要拦截的目标，**`handler`**参数也是一个对象，用来定制拦截行为。

```javascript
let proxy = new Proxy({
    
	// 所有对该对象的访问都将通过proxy对象实现
}, {
	get: function(target, property) {
		return 35 
	}
})
proxy.name // 35
proxy.age // 35
proxy.sex // 35
```

​	如果**`handler`**没有设置任何拦截，那就等同于直接通向原对象。

```js
let target = {}
let handler = {}
let proxy = new Proxy(target, handler)

proxy.a = "b"
target.a // 'b'

/*
*	在上面的代码中，handler是一个空对象，没有任何拦截效果，访问proxy就等同于访问target
*/
```

---

### 方法

​	**`Proxy`**原生支持13种拦截操作。

#### handler.get()

​	用于定义拦截对象的**`读取`**操作，**`get()`**方法可以返回任何值。

> 语法：
>
> ```javascript
> var proxy = new Proxy({}, {
> 	get: function(target, property, receiver) {
> 		// code...
> 	}
> })
> ```
>
> 参数：
>
> * **`target`** ：目标对象；
> * **`property`**：要获取的属性名；
> * **`receiver`**：源对象，Proxy或者继承Proxy的对象。

```javascript
let obj = {
	a: 1,
	b: 2
}

let proxy = new Proxy(obj, {
	get: function(target, key) {
        
		// 设置返回值，可以是任意值
		// return 20  
		return target[key]
	}
})

// proxy.a, 20
// proxy.b, 20

obj.a // 1
obj.b // 2 
```

---

#### handler.set()

​	用于定义拦截对象**`设置属性值`**的操作，set方法应该返回一个**`布尔值`**，返回true代表此次设置属性成功了，如果返回false且设置属性操作发生在严格模式下，那么会抛出一个`TypeError`。

> 语法：
>
> ```javascript
> let proxy = new Proxy({}, {
> 	set: function(target, property, value, receiver) {
> 		// code...
> 	}
> })
> ```
>
> 参数：
>
> ​		以下是传递给set方法的参数，`this上下文绑定在`handler对象上.
>
> * **`value`** ：被设置的属性值；
> * **`receiver`**：最初被调用的对象。通常是proxy本身，但handler的set方法也有可能在原型链上或以其他方式被间接地调用（因此不一定是proxy本身）。

```javascript
let obj = {
	a: 1,
	b: 2
}
let proxy = new Proxy(obj, {
	set: function(target, key, value) {
		return 
	}
})
obj.a = 3 
```

---

### this问题

​	虽然Proxy可以代理针对目标对象的访问，但它不是目标对象的透明代理，即不做任何拦截的情况下，也无法保证与目标对象的行为一致。主要原因就是在Proxy代理的情况下，目标对象内部的**`this`**关键字会指向Proxy代理。

```javascript
const targrt = {
	m: function() {
		console.log(this === proxy)
	}
}
const handler = {}
const proxy = new Proxy(target, handler)

target.m() // false
proxy.m() // true

/*
*	一旦proxy代理target.m,后者内部的this就是指向proxy，而不是target
*/
```

---

### Proxy的用途

#### 双向数据绑定

```js

```

