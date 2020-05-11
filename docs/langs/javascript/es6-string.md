# String拓展

​	传统上，JavaScript只有**`indexof()`**方法，可以用来确实一个字符串是否包含在另一个字符串中，es6又提供了三种新方法。

### includes()

​	用于判断一个字符串是否包含在另一个字符串中，根据情况返回**`true`**或 **`false`**，该方法区分大小写。

> 语法：
>
> ```css
> str.includes(searchString[, start])
> ```
>
> 参数：
>
> * **`searchString`**：要在此字符串中搜索的字符串。
>
> * **`start`**(可选)：从当前字符串的哪个索引位置开始搜寻子字符串，默认值为**`0`**。
>

```javascript
var str = 'hello world'
str.includes('world', 3) // true
```

```js
/*
* Polyfill
*/ 	
if (!String.prototype.includes) {
	String.prototype.includes = function(search, start) {
		'use strict'
      	
		// 设置第二个参数默认值
		if (typeof start !== 'number') {
			start = 0
		}
      	
		if (start + search.length > this.length) {
			return false
		} else {
			return this.indexof(search, start) !== -1
		}
	}
}
```

---

### startsWith()

​		用来判断当前字符串是否以另外一个给定的子字符串开头，并根据判断结果返回 **`true`** 或**`false`**，该方法区分大小写。

> 语法：
>
> ```css
> str.startsWith(searchString[, start])
> ```
>

```javascript
var str = 'hello baby'
str.startsWith('hello') // true
```

```js
// 结合第二个参数，能够判断特定位置的字符
var str = "转瞬即逝的涟漪，是深海水草的大口喘气"

str.startsWit('涟漪', 5) // 判断5号位的字符是否为 '涟漪'
```

```js
// Polyfill
if (!String.prototype.startsWith) {
	Object.defineProperty(String.prototype, 'startsWith', {
		value: function(search, pos) {
			pos = !pos || pos < 0 ? 0 : +pos;
			return this.substring(pos, pos + search.length) === search;
		}
	})
}
```

---

### endsWith()

​	用来判断当前字符串是否是以另外一个给定的子字符串“结尾”的，根据判断结果返回 **`true`** 或 **`false`**，该方法区分大小写。

> 语法：**`str.endsWith(searchString[, length])`**
>
> length：可选，作为str的长度，默认值为str.length。

```javascript
var str = 'hello baby'
str.endsWith('baby') // true
```

```js
// Polyfill
if (!String.prototype.endsWith) {
	String.prototype.endsWith = function(search, this_len) {
		if (this_len === undefined || this_len > this.length) {
			this_len = this.length
		}
		return this.substring(this_len - search.length, this_len) === search
	}
}
```

---

### repeat()

​	构造并返回一个新字符串，该字符串包含被连接在一起的指定数量的字符串的副本。

> 语法：
>
> ```js
> var new_arr = str.repeat(count)
> ```
>
> 参数：
>
> * **`count`**：介于0和正无穷大之间的整数 : [0, +∞) 。表示在新构造的字符串中重复了多少遍原字符串。
>     * count如果是小数，会被向下取整；
>     * count如果是负数或者infinity，会报错；
>     * 0 到-1之间的小数，等同于0，这是因为会先进行取整运算。0到-1之间的小数，取整运算之后是-0，**`repeat()`**视为0；
>     * count如果是NaN，等同于0；
>     * count值如果是字符串，则先转为数字。
>

```javascript
var str = 'alice'
var restr = str.repeat(3)
console.log(restr) // 'alicealicealice'
```

