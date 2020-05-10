# Array对象

### 属性

#### length

​		length属性用于**`设置`**或者**`返回`**数组中元素的数目。

> 语法：
>
> ```css
> /* 设置数组的长度 */
> arr.length = number
> 
> /* 返回数组的长度 */
> arr.length
> ```
>

```javascript
var arr = [1, 2, 3]

// 返回数组的长度
arr.length // 3

// 设置数组的长度
arr.length = 4
arr // [1, 2, 3, empty]

// 修改数组
arr.length = 2
arr // [1, 2]

// 清除数组
arr.length = 0
arr // []
```

---

#### [index]

​	**`获取`**或者**`修改`**数组指定索引下的值。

> 语法：
>
> ```css
> /* 获取数组指定索引的值 */
> arr[index]
> 
> /* 修改数组指定索引的值 */
> arr[index] = value
> ```
>

```javascript
// 修改数组指定索引下的值
var arr = [1, 2, 3, 4]

arr[1] = 'alice'
arr // [1, 'alice', 3, 4]
```

---

### 方法

#### Array.isArray()

​	检测传入的值是否为一个**`Array`**，返回一个**`布尔值`**。

> 语法：
>
> ```css
> Array.isArray(obj)
> ```
>

```javascript
// isArray()用于检测一个值是否是Array

var str = '123'
var arr = []

// 是数组，返回true
Array.isArray(arr) // true

// 不是数组，返回false
Array.isArray(str) // false
```

---

#### toString()

​	将数组转为字符串，并返回结果。

> 语法：
>
> ```css
> arr.toString()
> ```
>

```javascript
// toString()用于把数组转为字符串
var arr = [1, 2, 3, 4]

arr.toString() // '1,2,3,4'
```

---

#### concat()

​	将两个或多个数组拼接到一块，并返回拼接好的数组副本。

> 语法：
>
> ```css
> arr.concat(arr1, arr2, ..., arrX)
> ```
>

```javascript
// concat()用于拼接数组
var arr1 = [1, 2]
var arr2 = [3, 4]
arr1.concat(arr2) // [1, 2, 3, 4]
```

---

#### ☂ indexOf()

​	返回某个指定元素在数组中**`首次出现的位置`**，如果在数组中没有找到指定元素则返回**`-1`**。

> 语法：
>
> ```css
> arr.indexOf(item, start)
> ```
>
> 参数：
>
> * **`item`**： 要查找的元素；
>
> * **`start`**(可选)：规定在数组中开始检索的位置，合法值**`0 ～ arr.length - 1`**，默认为**`0`**。
>
> * **`该方法不兼容IE8及以下`**
>

```javascript
// indexOf()用于在数组中查找指定元素
var arr = [1, 2, 'alice', 3, function fn(){}]

// 默认从0开始检索
arr.indexOf(3) // 3

// 查找失败返回-1
arr.indexOf('box') // -1

// 查找使用 ===
arr.indexOf(function fn(){}) // -1
```

---

#### ☂ lastIndexOf()

​	返回某个指定元素在数组中**`最后出现的位置`**。

> 语法：
>
> ```css
> arr.lastIndexOF(item, start)
> ```
>
> 参数：
>
> * **`该方法不兼容IE8及以下`**
>

```javascript
// lastIndexOf()用于匹配元素在数组中最后出现的位置
var arr = [1, 3, 2, 4, 3]

arr.lastIndexOf(3) // 4
```

---

#### valueOf()

​	返回Array对象的原始值。

> 语法：
>
> ```css
> arr.valueOf()
> ```
>

```javascript
// valueOf()返回Array对象的原始值
var arr = [1, 2, 3, 4]

arr.valueOf() // [1, 2, 3, 4]
```

---

#### slice()

​	截取现有数组中的某个数组片段并将其作为新的数组返回。

> 语法：
>
> ```css
> arr.slice(start, end)
> ```
>

```javascript
// slice()用于切割数组
var arr = ['alice', 1, 2, 3, 'boss']

// slice()可以用于复制数组
arr.slice() // ["alice", 1, 2, 3, "boss"]

// ''
arr.slice('') // ["alice", 1, 2, 3, "boss"]

// 省略end，则默认切完
arr.slice(2) // [2, 3, "boss"]

// 前闭后开
arr.slice(0, 2) // ["alice", 1]

// 可以为负数
arr.slice(-3, -1) // [2, 3]
```

---

#### join()

​	把数组中的所有元素转换为一个字符串。

> 语法：
>
> ```css
> arr.join(separator)
> ```
>
> 参数：
>
> * **`separator`**(可选):  指定要使用的分隔符，如果省略，则默认使用逗号**`,`**。
>

```javascript
// join()用于将数组转为字符串
var arr = [1, 2, 3, 4, 'alice']

// 默认使用逗号做分隔符
arr.join() // '1,2,3,4,alice'

// 指定分隔符
arr.join(';') // '1;2;3;4;alice'

arr.join('a') // '1a2a3a4aalice'

arr.join('') // '1234alice'
```

---

#### ☂✵ unshift()

​	往数组的**`头部`**添加一个或多个元素，并返回新的**`数组长度`**，该方法会**`改变源数组`**

> 语法：
>
> ```css
> arr.unshift(item1, item2, ..., itemX)
> ```
>
> 参数：
>
> * **`该方法不兼容IE8`**
>

```javascript
// unshift()用于向数组的头部添加元素
var arr = [2, 3, 4]

// unshift()
arr.unshift(1) // 4
arr // [1, 2, 3, 4]

// 会区分字符串
arr.unshift('1')
arr // ["1", 2, 3, 4]
```

---

#### ✵ shift()

​	删除数组中的第一个元素，并返回**`被删除元素的值`**，该方法会**`改变源数组`**。

> 语法：
>
> ```css
> arr.shift()
> ```
>

```javascript
// shift()用于删除数组的第一个元素
var arr = [1, 2, 3, 4]

arr.shift() // 1
arr // [2, 3, 4]
```

---

#### ✵ push()

​		向数组的尾部添加一个或多个元素，并返回新的**`长度`**，该方法会**`改变源数组`**。

> 语法：
>
> ```css
> arr.push(item1, item2, ..., itemX)
> ```
>

```javascript
// push()用于向数组尾部添加元素
var arr = [1, 2, 3, 4]

// 使用push
arr.push('alice') // 5
arr // [1, 2, 3, 4, "alice"]

// 也可以使用concat
arr.concat('alice') // [1, 2, 3, 4, "alice", "alice"]
```

---

#### ✵ pop()

​	删除数组的最后一个元素，并返回**`被删除的元素`**，该方法会**`改变源数组`**。

> 语法：
>
> ```css
> arr.pop()
> ```
>

```javascript
// pop()用于删除数组的最后一个元素
var arr = [1, 2, 3, 4, 'alice']

arr.pop() // 'alice'
arr // [1, 2, 3, 4]
```

---

#### ✵ splice()

​	删除或添加数组中任意位置的元素，并返回**`被删除的元素数组`**；如果仅删除一个元素，则返回一个元素的数组；如果未删除任何元素，则返回空数组。该方法会**`改变源数组`**。

> 语法：
>
> ```css
> arr.splice(index, howmany, item1, item2, ..., itemX)
> ```
>
> 参数：
>
> * **`index`**:  规定从何处添加或者删除元素，该参数为下标，必须是数字；
>
> * **`howmany`**(可选):  规定应该删除多少个元素，必须是数字(可以是'0')，默认：**`删除index到结尾的所有元素`**;
>
> * **`item`**(可选):  要添加到数组的新元素。
>

```javascript
// splice()用于向数组中添加或删除元素
var arr = [1, 2, 3, 4]

// pop()
arr.splice(arr.length - 1, 1) // [4]
arr // [1, 2, 3]

// unshift()
arr.splice(0, 0, 'alice') // []
arr // ['alice', 1, 2, 3, 4]

// 省略howmany可以删除所有元素
arr.splice(0) // [1, 2, 3, 4]
arr // []

// 省略howmany不能添加元素
arr.splice(0, 'alice') // []
arr // [1, 2, 3, 4]
```

---

#### ✵ reverse()

​		用于颠倒数组中元素的顺序，并将颠倒后的数组作为结果返回出来，该方法**`会改变源数组`**。

> 语法：
>
> ```css
> arr.reverse()
> ```
>

```javascript
// reverse()用于颠倒数组中元素的顺序
var arr = [1, 2, 3, 4]

arr.reverse() // [4, 3, 2, 1]
arr // [4, 3, 2, 1]

// 反转字符串
var str = 'abcde'
var s1 = str.split('').reverse().join('')
s1 // 'edcba'
```

---

#### ✵ sort()

​		用原地算法对数组的元素进行排序，并返回数组，该方法**`会改变源数组`**，sort排序不一定是稳定的，默认排序顺序是根据字符串的unicode码点。

> 语法：
>
> ```css
> arr.sort(compareFunction(firstEl, secondEl))
> ```
>
> 参数：
>
> * **`compareFunction`**(可选) ：用来指定按照某种顺序进行排列的函数，如果省略，元素按照转换为的字符串的各个字符的Unicode位点进行排序。
>     * **`firstEl`**：第一个用于比较的元素；
>     * **`secondEl`**:第二个用于比较的元素。
>

```javascript
// sort()用于对数组进行排序

var arr = [1, 5, 2, 10, 3, 60, 4]

// ascending sort
arr.sort((a, b) => a - b)  // [1, 2, 3, 4, 5, 10, 60]

// descending sort
arr.sort((a, b) => b - a) // [60, 10, 5, 4, 3, 2, 1]

// inverted sort
arr.sort((a, b) => 1) // b在a前面
// [1, 5, 2, 10, 3, 60, 4]
```

---

#### forEach()

​	遍历数组。对数组的每个元素执行一次提供的函数。

​		**`forEach`**方法按升序为数组中含有效值的每一项执行一次**`callback`**函数，那些已删除或者未初始化的项将被跳过（例如在稀疏数组上）。

​		**`callback`**函数会被依次传入三个参数：

* 数组当前项的值；

* 数组当前项的索引；

* 数组对象本身。

> 语法：
>
> ```css
> arr.forEach(callback(value, index, arr), thisAry)
> ```
>

```javascript
// forEach()用于便利数组
var arr = [1, 2, 3, 4]

arr.forEach((v, i, a) => {
	console.log(v)
})
// 1
// 2
// 3
// 4
```

---

#### filter()

​	过滤数组，返回过滤后的**`新数组`**，新数组中的元素是通过检查指定数组中符合条件的所有元素。如果没有任何元素通过测试，则返回**`[]`** 。

​		**`filter` **为数组中的每个元素调用一次 **`callback` **函数，并利用所有使得 **`callback` **返回 **`true`** 或 **`等价于true的值`** 的元素创建一个新数组。**`callback` **只会在已经赋值的索引上被调用，对于那些已经被删除或者从未被赋值的索引不会被调用。那些没有通过 **`callback`** 测试的元素会被跳过，不会被包含在新数组中。

​		**`callback`** 被调用时传入三个参数：

* 数组的值；

* 数组的索引；

* 被便利数组本身；

> 语法：
>
> ```css
> var new_array = arr.filter(callback(element[, index[, arr] ] ), thisAry)
> ```
>
> 参数：
>
> * **`callback`** ：用来测试数组的每个元素的函数。返回 **`true`** 表示该元素通过测试，保留该元素，**`false` **则不保留。它接受以下三个参数：
>     * **`element`**(可选)：数组中当前正在处理的元素；
>     * **`index`**(可选)：正在处理的元素在数组中的索引;
>     * **`array`**(可选)：调用了**`filter`**的数组本身。
>
> * **`thisAry`**：如果为 **`filter`** 提供一个 **`thisArg`** 参数，则它会被作为 **`callback`** 被调用时的 **`this`** 值。否则，**`callback`** 的 **`this`** 值在非严格模式下将是全局对象，严格模式下为 **`undefined`**。
>

```javascript
// filter()用于过滤数组
var arr = ['ambition', 'paino', 'mother', 'change', 'consider']

// 返回长度大于7的字符串
function checkLength (word) {
	return word.length >= 7
}

var newAry = arr.filter(checkLength) //回调函数不能加括号 
// ["ambition", "consider"] 
```

---

#### map()

​	处理数组，返回一个新数组，数组元素为源数组中的元素调用提供的函数处理后的值。

> 语法：
>
> ```css
> var new_array = arr.map(callback(value, index, arr), thisAry)
> ```
>
> 参数：
>
> * **`callback`** ：生成新数组元素的函数。
>

```javascript
// map()用于处理数组
var arr = [1, 2, 3, 4]

arr.map((value) => {
	return value * 2
}) // [2, 4, 6, 8]
```

---

#### every()

​	测试一个数组内的**`所有元素`**是否都能通过某个指定函数的测试，返回一个布尔值。如果接收一个空数组，则此方法在一切情况下都会返回**`true`**。

​		只有有一个值没有通过测试，就返回**`false`**。

> 语法：
>
> ```css
> arr.every(callback(element, index, arr), thisAry)
> ```
>

```javascript
// every()用于测试数组内的元素是否能通过指定函数的测试

var arr = [0, 10, 15, 27, 39]

function isBlowThreshold(currentValue) {
	// checks whether an element is less than 40
	return currentValue < 30
}

arr.every(isBlowThreshold) // false
```

---

#### some()

​		测试一个数组内是不是**`至少有一个元素`**通过了指定函数的测试，返回一个布尔值。如果用一个**`空数组`**进行测试，则在任何情况下它的返回值都是**`false`**。

> 语法：
>
> ```css
> arr.some(callback(element, index, arr), thisAry)
> ```
>

```javascript
// some()用于测试数组内是否至少有一个元素能通过指定函数的测试
var arr = [3, 10, 15, 27, 39]

function even (value) {
	// checks whether an element is even
	return value % 2 === 0
}
arr.some(even) // true
```

---

#### find()

​	返回数组中满足提供的测试函数的第一个元素的**`值`**，否则返回**`undefined`**。

> 语法：
>
> ```css
> arr.find(callback(element, index, arr), thisAry)
> ```
>

```javascript
// find()用于查找满足测试函数的第一个元素的值

var arr = [0, 2, 4, 6, 8]

arr.find((value) => {
	return value > 5
}) // 6
```

---

#### findIndex()

​	返回数组中满足提供的测试函数的第一个元素的**`索引`**，否则返回**`-1`**。

> 语法：
>
> ```css
> arr.findIndex(callback(element, index, arr), thisAry)
> ```
>

```javascript
// findIndex()用于查找满足测试函数的第一个元素的索引值
var arr = [0, 3, 6, 9, 11]

arr.findIndex((value) => {
	return value > 5
}) // 2 --> 返回6的索引值
```

