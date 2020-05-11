# Set数据结构

​	es6提供了新的数据结构**`Set`**。**`Set`**对象允许你存储任何类型的唯一值，无论是**`原始值`**或者是对象引用，它类似于数组，但是成员值都是唯一的，没有重复的值。

### 创建一个Set结构

​	Set本身就是一个构造函数，又来生成Set数据结构。

> 语法：
>
> **`new Set([iterable])`**
>
> 参数：
>
> * **`iterable`**（可选）：如果传递一个**`可迭代对象`**，它的所有元素将不重复地被添加到新的**`Set`**中。如果不指定此参数或其值为null，则新的**`Set`**为空。

```javascript
let set = new Set()

;[1, 4, 2, 3, 1, 2].forEach(x => set.add(x))

console.log(set) // {1, 4, 2, 3}
// 通过add方法像Set结构添加成员，结果表明Set结构不会添加重复的值
```

​	Set函数可以接收一个数组作为参数，用来初始化，但是**`不能`**够接收**`类数组`**。

```javascript
// 例1: 
const set = new Set([1, 2, 3, 4, 4])
[...set] // [1, 2, 3, 4]

// 例2:
const item = new Set([1, 2, 3, 4, 5, 5, 5])
item.size // 5

// 例3: 类数组先转为数组
function divs() {
	return [...document.getElementsByTagName('div')]
}
const set = new Set(divs())
set.size // 12

// 类似于
divs().forEach(div => set.add(div))
set.size // 12
```

---

### 属性

#### constructor

​	**`constructor`**属性返回实例的构造函数，默认就是**`Set`**。

```javascript
const set = new Set([1, 2, 3, 4, 5])
set.constructor() // ƒ Set() { [native code] }
```

---

#### size

​	**`size`**属性将会返回**`Set`**对象中元素的个数。

```javascript
const set = new Set([1, 2, 3, 4, 5])
set.size // 5
```

---

### 方法

​	Set 实例有以下 7 个方法：包含 4 个操作方法和 3 个遍历方法。

#### add()

​	**`add()`** 方法用来向一个**`Set`**对象的末尾添加一个指定的值，返回值：Set对象本身(意味着可以进行链式操作)。

> 语法：
>
> **`set.add(value)`**
>
> 参数：
>
> * **`value`**（必需）：要添加到Set对象的元素的值。

```javascript
var set = new Set()

// 链式操作
set.add(1).add('2')
console.log(set) // {1, "2"}
```

---

#### clear()

​	**`clear()`**方法用来清空一个**`Set`**对象中的所有元素，返回值：undefined。

> 语法：
>
> **`set.clear()`**

```javascript
var set = new Set([1, 2, 3, 4, 5])
set.size // 5

set.clear() 
set.size // 0
```

---

#### delete()

​	**`delete()`**方法可以从一个**`Set`**对象中删除指定的元素，删除成功则返回true，失败则返回false。

> 语法：
>
> **`set.delete(value)`**
>
> 参数：
>
> * **`value`**：要求删除的元素。

```javascript
var set = new Set(['alice', 'alien', 1, 4, 5])

set.delete('alice') // true
set // {"alien", 1, 4, 5}

// 再次删除'alice'
set.delete('alice') // false
```

---

#### has()

​	**`has()`**方法用于判断一个元素是否存在于**`Set`**对象中，存在则返回true，不存在则返回false。

> 语法：
>
> **`set.has(value)`**
>
> 参数：
>
> * **`value`**(必需)：用以测试该值是否存在于 Set 对象中。

```javascript
var set = new Set(['alice', 'alien', 1, 4, 5])

set.has('alice') // true
```

---

### Set数据结构的用途

#### 数据去重

```js
let arr = [1, 2, 3, 4, 5, '5', 1, 4, 3]

[...new Set(arr)] // [1, 2, 3, 4, 5, "5"]

/*
*	1. 向Set中加入值的时候，不会发生类型转换，所以5和'5'是两个值
*	
*	2. Set内部判断两个值不同，使用的算法叫'Same-value equality'，它类似于精确相等运算符（===），主要区别是NaN等于自身，而精确相等运算符NaN不等于自身。
*/
```

---

#### 字符串去重

```js
var str = 'ababbc'
[...new Set(str)].join('') // 'abc'
```

---

### Array.from()

​	**`Array.from()`**可以将**`Set`**结构转为**`数组`**。

```javascript
const set = new Set([1, 2, 3, 4, 5])

Array.from(set) // [1, 2, 3, 4, 5]

// 或者使用拓展运算符
[...set] // [1, 2, 3, 4, 5]
```

