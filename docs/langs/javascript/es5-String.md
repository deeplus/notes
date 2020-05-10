# String对象

​	字符串（String）即文本，**`字符串方法都不会修改源字符串`**。

### 字符串拼接

​	在 es5 中，字符串的拼接通过**`+`**来完成，字符串由**` ''`**包裹，变量无需包裹。

```html
// 字符串拼接
<div>123</div>
<script>
	var box = document.getElementById('box')
	box.onclick = function(){
		box.innerHTML = box.innerHTML + '123'
		// 等价于 
		box.innerHTML += '123'
	}
</script>
```

---

### 属性

#### length

​	**`length`**属性返回字符串的长度，空字符串的**`length`**为0。注意：**`空格字符会被解析`**。

> 语法：
>
> ```css
> str.length
> ```
>

```js
// 空格字符串会被解析
'123 12'.length // 6

// 空字符串的length为0
''.length // 0
```

---

### 方法

#### toString()

​	返回一个**`String`**对象的值。

> 语法：
>
> ```css
> str.toString()
> ```
>

```javascript
// toString()方法返回一个String对象的值
var str = "alice"

str.toString() // 'alice'
```

---

#### charAt()

​	返回在指定位置的字符串，该方法兼容所有浏览器。

> 语法：
>
> ```css
> str.charAt(index)
> ```
>

```javascript
// 字符串可以通过下标取值，但仅支持主流浏览器，在垃圾浏览器里用不了
var str = "abcde"
str[3] // d 

// charAt()能够在所有浏览器环境使用
str.charAt(0) // a 
```

---

#### concat()

​	将两个或多个字符串拼接到一块，并返回拼接好的字符串。

> 语法：
>
> ```css
> str.concat(str1, str2, ..., strX)
> ```
>

```javascript
// concat()拼接字符串

var str = '小姣'.concat('是', '一只猪') // 小姣是一只猪

// +拼接
var str = '小姣' + '是' + '一只猪' // 小姣是一只猪
```

---

#### indexOf()

​	返回某个指定的字符串在字符串中**`首次出现的位置`**，如果没有找到匹配的字符串则返回**`-1`**，该方法**`对大小写敏感`**,查找时使用**`===`**。

> 语法：
>
> ```css
> str.indexOf(searchValue, start)
> ```
>
> 参数：
>
> * **`searchValue`**：指定要查找的字符串；
>
> * **`start`**：规定在字符串中开始检索的位置，合法值是**`0 ~ str.length - 1`**，默认为**`0`**。
>

```javascript
// indexOf()查找指定字符串首次出现的位置
var str = "ambition"

// 默认从0开始检索
str.indexOf('m') // 1 

// 查找失败返回-1
str.indexOf('m', 2) // -1

// 该方法对大小写敏感
str.indexOf('M', 0) // -1


// 手写一个函数实现indexOf()

function indexof(str, target) {
	for (let i = 0; i < str.length; i ++) {
		if(str[i] === target){
			return i
		}
	}
	return -1
}
var str = 'alice'
indexof(str, 'e') // 4
```

---

#### lastIndexOf()

​	返回某个指定的字符串在字符串中**`最后出现的位置`**，如果没有找到匹配的字符串则返回**`-1`**，该方法同样**`区分大小写`**。

​	该方法是从后往前检索，但返回值是从前往后计算。

> 语法：
>
> ```css
> str.lastIndexOf(searchValue, start)
> ```
>
> 参数：
>
> * **`start`**：合法取值是**`0 ~ str.length - 1`**，默认为**`str.length`**。
>

```javascript
// lastIndexOf()查找指定字符串最后出现的位置
var str = "ambition"

// 默认从str.length-1开始检索
str.lastIndexOf('i') // 5

// 查找失败返回-1
str.lastIndexOf('i', 2) // -1


// 手写一个函数实现lastIndexOf()
function lastindexof(str, target) {
	for(let i = str.length - 1; i >= 0; i--) {
		if(str[i] === target){
			return i
		}
	}
	return -1
}
var str = "dcbc"
lastindexof(str, 'c') // 3
```

---

#### valueOf()

​	返回字符串对象的原始值。

> 语法：
>
> ```css
> str.valueOf()
> ```
>
> 参数：
>
> * 该方法通常由JavaScript在后台自动进行调用，而不是显式地处于代码中。
>

```javascript
// valueOf()方法返回string对象的原始值
var str = 'alice'

str.valueOf() // 'alice'
```

---

#### charCodeAt()

​	返回指定位置的字符的Unicode编码。

> 语法：
>
> ```css
> str.charCodeAt(index)
> ```
>

```javascript
// charCodeAt()返回指定位置字符的unicode编码

var str = "alice"

str.charCodeAt(3) // 99 -->字母c的unicode编码
```

---

#### String.fromCharCode()

​	返回指定unnicode码所对应的字符串。

> 语法：
>
> ```css
> String.fromCharCode(n1, n2, ..., nX)
> ```
>

```javascript
// fromCharCode()返回指定unicode码对应的字符串

String.fromCharCode(99) // c 
```

---

#### slice()

​	截取字符串中介于两个下标之间的字符，并返回新的字符串。

> 语法：
>
> ```css
> str.slice(start, end)
> ```
>
> 参数：
>
> * 该方法**`会从左往右`**截取字符串，包括start，但是不包括end；**`[start, end)`**
>
> * start、end的值**`可以取负数`**，如果是负数，则规定该参数是从字符串的尾部开始算，即-1指字符串的最后一个字符，-2指字符串的倒数第二个字符，依次类推。
>
> * **`该方法start、end无论在什么时候都不会交换位置，截取到则有值，截取不到则无值`**。
>

```javascript
// slice()截取字符串的某个部分

var str = "alice"

// 省略end，则默认从start开始，截取完剩余字符串
str.slice(2) // ice

// 前闭后开
str.slice(0, 2) // al

// 无论何种情况，start与end不会交换位置
str.slice(3, 0) // 截取不到 --> 无值
str.slice(-3, 1) // --> 这种情况也截取不到，相当于str.slice(2, 0)

// 参数为负数，表示从后往前算
str.slice(0, -2) // ali
```

---

#### substring()

​	截取字符串中介于两个下标之间的字符。

> 语法：
>
> ```css
> str.substring(start, end)
> ```
>
> 参数：
>
> * 该方法会**`从左往右`**截取字符串，包括from，但不包括to；**`[start, end)`**	
>
> * **`该方法如果start值比end值大，则在提取子串之前会先交换这两个数`**。
>

```javascript
// substring()截取介于两个下标之间的字符
var str = "alice"

// 省略end，则默认从start开始，截取完剩余字符串
str.substring(2) // ice

// 前闭后开
str.substring(0, 2) // al

// 如果start比end大，则截取之前先交换位置
str.substring(3, 0) // ali
```

---

#### substr()

​		截取字符串中指定下标开始指定数目的字符。

> 语法：
>
> ```css
> str.substr(start, length)
> ```
>
> 参数：
>
> * start的值可以取负数，如果取负数，则表示从字符串的尾部开始算，即-1表示最后一个字符，依次类推。

```javascript
// substr()截取字符串中指定下标开始指定数目的字符
var str = "alice"

// 省略length，则默认返回从start开始到结束的字符串
str.substr(2) // ice

// 截取一个长度片段
str.substr(2, 2) // ic

// satrt可以为负数
str.substr(-3, 2) // ic
```

```css
如何证明substr截取的是一个字符串的长度?

var str = 'ambition'

str.slice(1, 2) // 'm'
str.substring(1, 2) // 'm'
str.substr(1, 2) 'mb'
```

---

#### toLocaleLowerCasse()

​	根据本地主机的语言环境把字符串转为小写。本地是根据浏览器的语言设置来判断的。

> 语法：
>
> ```css
> str.toLocaleLowerCase()
> ```
>

```javascript
// toLocaleLowerCase()将字符串转为小写
var str = "ALICE"

str.toLocaleLowerCase() // alice
```

---

#### toLocaleUpperCase()

​	根据本地主机的语言将字符串转为大写。

> 语法：
>
> ```css
> str.toLocaleUpperCase()
> ```
>

```javascript
// toLocaleUpperCase()将字符串转为大写
var str = "alice"

str.toLocaleUpperCase() // ALICE
```

---

#### toLowerCase()

​	把字符串转为小写。

> 语法：
>
> ```css
> str.toLowerCase()
> ```
>

```javascript
// toLowerCase()将字符串转为小写
var str = "ALICE"

str.toLowerCase() // alice
```

---

#### toUpperCase()

​	把字符串转为大写。

> 语法：
>
> ```css
> str.toUpperCase()
> ```
>

```javascript
// toUpperCase()将字符串转为大写
var str = "alice"

str.toUpperCase() // ALICE
```

---

#### ☂ trim

​	删除字符串头尾空格，该方法不兼容垃圾浏览器。

> 语法：
>
> ```css
> str.trim()
> ```
>

```javascript
// trim()方法用于删除字符串两端的空格
var str = " ali ce  "

str.trim() // 'ali ce'
```

---

#### split()

​	把一个字符串**`分割`**成**`字符串数组`**，返回分割后的数组。

> 语法：
>
> ```css
> str.split(separator, limit)
> ```
>
> 参数：
>
> * **`separator`** (可选)：字符串或正则表达式；
>
> * **`limit`** (可选)：指定返回数组的最大长度，最大为**`str.length - 1`**，默认**`str.length -1`**。
>

```javascript
// split()把字符串分割成字符串数组
var str = "ambition"

// 不传值
str.split() // ["ambition"]

// 空字符串
str.split('') // ["a", "m", "b", "i", "t", "i", "o", "n"]

// 以i字符进行切割
str.split('i') // ["amb", "t", "on"]
```

---

#### match()

​	在字符串内检索指定的值，或找到一个或多个正则表达式的匹配。其返回值为一个数组，数组的内容取决于global（**`g`**）标志的存在与否，如果未找到匹配则为**`null`**。

​	该方法类似**`indexOf()`**和**`lastIndexOf()`**，但是它返回指定的值，而不是字符串的位置：

* 如果正则表达式不包含**`g`**标志，**`string.match()`** 将返回与**`regexp.exec()`**相同的结果。

> 语法：
>
> ```css
> str.match(regexp)
> 
> // 或者
> str.match(searchValue)
> ```
>

```javascript
var str = 'alice12345678'
var reg = /\d{3, 10}/g

str.match(reg) // ["12345678"]
```

---

#### replace()

​	返回一个由替换值（replacement）替换一些或所有匹配的模式（pattern）后的新字符串。模式可以是一个字符串或者一个正则表达式，替换值可以是一个字符串或者一个每次匹配都要调用的回调函数。

> 语法：
>
> ```css
> str.replace(regexp|substr, newSubStr|function)
> ```
>
> 参数：
>
> * **`regexp`**(pattern) ：一个RegExp对象或其字面量，满足规则的内容会被第二个参数替换掉；
>
> * **`substr`** (pattern) ：一个将被第二个参数替换的字符串，其被视为一整个字符串，而不是一个正则表达式，仅第一个匹配项会被替换；
>
> * **`newSubStr`** (replacement)：用于替换掉第一个参数在原字符中的匹配部分的字符串。该字符串中可以内插一些**`特殊的变量名`**；
>
> * **`function`** (replacement)：一个用来创建新子字符串的函数，该函数的返回值将替换掉第一个参数匹配到的结果。
>

```javascript
var str = 'abc123def456'

str.replace('abc', '兔子') // '兔子123def456'

str.replace(/\D{3}/g, '兔子') // 兔子123兔子456
```

