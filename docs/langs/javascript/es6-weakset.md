# WeakSet

​	**`WeakSet`**对象允许你将*弱保持对象*存储在一个集合中，WeakSet结构与Set结构类似，也是不重复的值的集合。但是，它与Set有两个区别：

* WeakSet的成员**`只能是对象（引用型）`**，而不能是其它类型的值**`(值类型)`**；
* WeakSet中的对象都是弱引用，即垃圾回收机制不考虑WeakSet对该对象的引用，也就是说：如果其它对象不再引用该对象，那么垃圾回收机制就会自动回收该对象所占用的内存，不考虑该对象还存在于WeakSet中。

​	由于上面这个特点，WeakSet的成员是不适合引用的，因为它会随时消失。另外，WeakSet内部有多少个成员，取决于垃圾回收机制有没有运行，运行前后很可能成员个数是不一样的，而垃圾回收机制何时运行是不可预测的，因此**`es6规定WeakSet不可遍历`**(没有遍历方法，只有操作方法，并且clear()方法已经废弃)。

---

### 创建一个WeakSet结构

​	通过构造函数WeakSet创建。

```javascript
// 这样做会直接报错
const ws = new WeakSet([1, 2, 3, 4]) // Uncaught TypeError: Invalid value used in weak set

// 正确的做法1:
const ws = new WeakSet([[1, 2], {a: '3'}]) // WeakSet {Array(2), {…}}

// 正确的做法2:
const ws = new WeakSet()
let arr = [1, 2]
let obj = {a: '3'}
ws.add(arr).add(obj) // WeakSet {Array(2), {…}}
```

---

### 属性

#### constructor

​	**`constructor`**属性返回实例的构造函数，即**`WeakSet`**本身。

```javascript
const ws = new WeakSet()
ws.constructor // ƒ WeakSet() { [native code] }
```

​	WeakSet没有**`size`**属性，没法遍历它的成员。

---

### 方法

​	WeakSet有3个操作方法。

#### add()

​	添加对象。

```javascript
let arr = [1, 2]
const ws = new WeakSet() // WeakSet {}
ws.arr(ws) // WeakSet {Array(2)}
```

---

#### delete()

​	删除对象。

```javascript
// 引用型不能删除
const ws = new WeakSet([[1, 2], {a: 1}]) // WeakSet {{…}, Array(2)}
ws.delete([1, 2]) // false
console.log(ws) // WeakSet {{…}, Array(2)}

// 正确的做法
let arr = [1, 2]
let obj = {a: 1}
const ws = new WeakSet() // WeakSet {}
ws.add(arr).add(oj) // WeakSet {{…}, Array(2)}
ws // WeakSet {Array(2), {…}}

ws.delete(obj) // true
ws // WeakSet {Array(2)}
```

---

#### has()

​	查询对象。

```javascript
// 引用型不能查询
const ws = new WeakSet([[1, 2], {a: 1}]) 
ws.has([1, 2]) // false

// 正确的写法
let arr = [1, 2]
const ws = new WeakSet() // WeakSet {}
ws.add(arr) // WeakSet {Array(2)}
ws.has(arr) // true
```
