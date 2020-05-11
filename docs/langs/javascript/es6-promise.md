# Promise

### 关于Promise

#### 概念

​	**`Promise`**对象用于表示一个异步操作的最终完成 (或失败)及其结果值。**`Promise`**是异步编程的一种解决方案，比传统的解决方案 -- 回调函数和事件 -- 更合理更强大。

---

#### 特点

*    对象的状态不受外界影响；
*    一旦状态改变，就不会再变，任何时候都可以得到这个结果。

---

#### 状态

​	**`Promise`** 对象是一个代理对象（代理一个值），被代理的值在Promise对象创建时可能是未知的。它允许你为异步操作的成功和失败分别绑定相应的处理方法（handlers）。 这让异步方法可以像同步方法那样返回值，但并不是立即返回最终执行结果，而是一个能代表未来出现的结果的promise对象。

​	一个**`Promise`**有以下三种状态：

*    **`pending`**(进行中)：初始状态，既不是成功也不是失败；
*    **`fulfilled`**(已成功)：意味着操作成功；
*    **`rejected`**(已失败)：意味着操作失败；

​	只有异步操作的结果，可以决定当前是哪一种状态，任何其它操作都无法改变这个状态；

---

#### 缺点

*    无法取消**`Promise`**，一旦新建它就会立即执行，无法中途取消；
*    如果不设置回调函数，**`Promise`**内部抛出的错误，不会反映到外部；
*    当处于**`pending`**状态时，无法得知目前发展到哪一个阶段（是刚刚开始还是即将完成）。

---

### 创建Promise

​	**`Promise`**对象是由关键字**`new`**及其构造函数来创建的。该构造函数会把一个叫做“处理器函数”（executor function）的函数作为它的参数。这个“处理器函数”接受两个函数——**`resolve`** 和 **`reject`**——作为其参数。当异步任务顺利完成且返回结果值时，会调用 **`resolve`**函数；而当异步任务失败且返回失败原因（通常是一个错误对象）时，会调用**`reject` **函数。

> 语法：
>
> ```javascript
> new Promise( function(resolve, reject) {...} /* executor */  );
> ```
>
> 参数：
>
> * **`executor`**：是一个处理器函数，接收**`resolve`**和**`reject`**两个函数作为参数，**`executor`**函数被调用发生在**`Promise`**构造函数返回所建promise实例对象之前。
>
> * **`Promise`**构造函数执行时会立即调用**`executor`**函数，**`resolve`**和**`reject`**两个函数作为参数传递给**`executor`**函数。
> * **`executor`**函数内部通常会执行一些异步操作，一旦异步操作执行完成（可能成功也可能失败）。如果执行成功，就会调用**`resolve`**函数来将**`Promise`**状态修改为**`fulfilled`**；如果执行失败，则调用**`reject`**函数来将**`Promise`**状态修改为**`rejected`**。
> * 如果在**`executor`**函数中抛出一个错误，那么该**`Promise`**的状态变为**`rejected`**，**`executor`**函数的返回值将被**`忽略`**。

```javascript
const promise = new Promise(function(resolve, reject){
	// 做一些异步操作，最终会调用下面两者之一：
    
	// resolve(someValue) // fulfilled
    
	// 或者
    
	// reject('failure reason') // rejected
})
```

---

### 方法

#### then()

​		**`then()`**方法返回一个**`全新的Promise对象`**，它最多需要接收两个回调函数（Promise成功的回调和失败的回调）。

> 语法：
>
> **`promise.then(onFulfilled[, onRejected])`**
>
> ```javascript
> // 也可以写成
> promise.then(value => {
> 	// value 接收 resolve的返回值
> }, err => {
> 	// err 接收 reject的返回值
> })
> ```
>
> 参数：
>
> * **`onFulfilled`**(可选))：当**`Promise`**变成接受状态（fulfilled）时调用的函数；
> * **`onReject`**(可选)：当 Promise 变成接受状态或拒绝状态（rejected）时调用的函数。

```javascript
new Promise((resolve, reject) => {
    
	setTimeout(() => {
		try {
			console.log('start')
			// 执行成功
			resolve(true)
		} catch (err) {
			// 执行失败
			reject(err)
		}           
	}, 100)
}).then(value => {
	// Promise执行成功，再次回调
	if (value) {
		setTimeout(() => {
			console.log('end')
		}, 10)
	}
}, err => {
	// Promise执行失败，打印错误，不会阻碍代码继续执行
	console.log(err)
})

// 'start'
// 'end'
```

---

#### catch()

​	**catch()** 方法返回一个**`全新的Promise`**对象，它只接收一个回调函数，用于处理Promise拒绝的情况。

> 语法：
>
> **`promise.catch(onRejected)`**
>
> ```javascript
> // 也可以写成
> promie.catch(err => {
> 	// 失败时候的处理函数
> })
> ```

```javascript
new Promise((resolve, reject) => {
    
	setTimeout(() => {
		try {
			console.log(a) // 本次代码执行失败
			resolve(true)
		} catch (err) {
			reject(err)
		}        
	}, 100)
}).catch(err => {
	// 处理错误信息，避免报错阻碍代码的后续执行
	console.log(err) // object: ReferenceError: a is not defined
})
```

---

#### Primise.all()

​	将多个Promise实例，包装成为一个新的Promise实例，通常用于发起**`并发请求`**。

> 语法：
>
> ```javascript
> const p = Promise.all([p1, p2, p3])
> ```
>
> 参数：
>
> * 参数为一个可迭代对象，可以是数组或字符串。
>
> 状态：
>
> ​		p的状态由p1，p2，p3决定，分为两种情况：
>
> * 只有p1，p2，p3的状态都变成**`fulfilled`**，p的状态才会变成**`fulfilled`**。此时p1，p2，p3的返回值组成一个数组，传递给p的回调函数。
> * 只要p1，p2，p3之中有一个被**`rejected`**，p的状态就变成**`rejected`**。此时第一个被rejected的实例的返回值，会传递给p的回调函数。
>

---

### 链式操作

​	由于**`then()`**和**`catch()`**方法都返回一个全新的**`Promise`**对象，意味着他们可以进行链式操作。

#### 向后续then传递成功信息

> 语法：
>
> ```javascript
> promise.then(value => {
> 	return value
> })
> ```
>
> 参数：
>
> * **`value`**：要传递的值。

```javascript
new Promise((resolve, reject) => {
	// 假设本次执行成功，直接触发then方法的成功回调
	resolve()
}).then(value => {
	return '事件2执行成功'
}).then(value => {
	console.log(value) // '事件2执行成功'
})
```

---

#### 向后续then传递错误信息

> 语法：
>
> ```javascript
> promise.then(value => {
> 	return new Promise((res, rej) => {rej(err)})
> })
> ```
>
> 参数：
>
> * **`err`**：要传递的错误信息。

```javascript
new Promise((resolve, reject) => {
	// 假设本次执行成功，直接触发then方法的成功回调
	resolve()
}).then(value => {
	return new Promise((res, rej) => {rej('事件2执行失败')})
}).catch(err => {
	console.log(err) // '事件2执行失败'
})
```

