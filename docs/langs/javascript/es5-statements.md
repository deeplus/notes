# 声明语句

### break

**`break语句`**表示终止当前循环（**`switch语句`**或者**`label语句`**），并把程序控制流转到紧接着被中止语句后面的语句。

> 语法：
>
> ```js
> break [label]
> ```
>
> 参数：
>
> * **`label`**：可选，与语句标签相关联的标识符。
>

```js
// 终止当前循环
for (var i = 0; i < 5; i++) {
	if(i === 3){
		break; // 因为i为3时，直接终止当前循环，所以3，4没有被打印出来
	}
	console.log(i)
}
// 0
// 1
// 2
```

---

### continue

**`continue 声明`**表示跳过本次循环，在下一次迭代时继续执行循环。

> 语法：
>
> ```javascript
> continue [label]
> ```
>

```javascript
// 跳过本次循环
for (var i = 0; i < 5; i ++) {
	if(i === 3){
		continue; // 因为i为3的时候跳过了本次循环，所以3没有被打印出来
	}
	console.log(i)
}
// 0
// 1
// 2
// 4
```

---

### return 



---

### try-catch

**`try...catch`**语句标记要尝试的语句块，并指定一个出现异常时抛出的响应。

> 语法：
>
> ```javascript
> try {
> 	try_statements
> } [catch (exception_var) {
> 	catch_statements
> }]
> ```
>
> 参数：
>
> * **`try_statements`**：需要被执行的语句；
> * **`exception_var`**：用于保存关联**`catch`**子句的异常对象的标识符；
> * **`catch_statements`**：如果在**`try`**块里有异常被抛出时执行的语句。
>

```javascript
try {
	console.log(a)
} catch (err) {
	console.log(err) // ReferenceError: a is not defined
}
```

