# Map数据结构

​		JavaScript的对象（Object），本质上是键值对的集合（Hash结构），但是传统上只能用字符串当作键，这给它的使用带来了很大的限制。

​		为了解决这个问题，es6提供了Map数据结构，**`Map`**对象用于保存键值对，任何值(对象或者**`原始值`**) 都可以作为一个键或一个值。Map结构类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说：Object结构提供了**`字符串——值的对应`**，Map结构提供了**`值——值`**的对应，是一种更完善的Hash结构的实现。如果你需要“键值对”的数据结构，Map比Object更合适。

---

### 创建一个Map结构

​	通过Map构造函数生成。

> 语法：
>
> ```js
> new Map([iterable])
> ```
>
> 参数：
>
> * **`iterable`**：Iterable 可以是一个数组或者其他 iterable 对象，其元素为键值对(两个元素的数组，例如: [[ 1, 'one' ],[ 2, 'two' ]])。 每个键值对都会添加到新的 Map。`null` 会被当做 `undefined。`

```javascript
const map = new Map()
const o = {a: 'hello'}
map.set(o, 'content')

console.log(map) // Map(1) {{…} => "content"}
```

​	作为构造函数，Map也可以接收一个数组作为参数，该数组的成员是一个个表示**`键值对`**的数组。

```javascript
const map = new Map([
	['name', '张三'],
	['title', 'Author']
])

console.log(map) // Map(2) {"name" => "张三", "title" => "Author"}
```

!> **`只有对同一个对象的引用，Map结构才将其视为同一个键`**，这一点要非常小心。

```js
const map = new Map()
map.set(['a'], 555) // Map(1) {Array(1) => 555}

map.get(['a']) // undefined
```

​		如果Map的键是一个简单类型的值（数字、字符串、布尔值），则只要两个值严格相等，Map就将其视为同一个键，比如**`0`**和**`-0`**是同一个键；**`true`**和**`'true'`**则是两个不同的键；另外，**`undefined`**和**`null`**也是两个不同的键；虽然**`NaN`**不严格等于其自身，但是Map将其视为同一个键。

```javascript
const map = new Map()
map.set(0, 'alice')
map.get(-0) // 'alice'

map.set(true, 'mdzz')
map.get('true') // undefined

map.set(undefined, 'ooo')
map.get(null) // undefined

map.set(NaN, 'ambition')
map.get(NaN) // 'ambition'
```

---

### 属性

#### constructor

​	返回实例的构造函数，默认**`Map`**。

```javascript
const map = new Map()
map.constructor // ƒ Map() { [native code] }
```

---

#### size

​	返回Map对象的成员个数，size 属性的值是一个整数，表示 Map 对象有多少个键值对。size 是只读属性，用set 方法修改size返回 undefined，即不能改变它的值。

```javascript
const map = new Map([
	['name', '张三'],
	['title', 'Author']
])

map.size // 2
```

---

### 与其它数组结构的相互转换

#### Map转数组

```js
const map = new Map()
	.set(true, 7)
	.set({foo: 3}, ['abc']);
[...map] // [[true, 7], [{foo: 3}, ['abc']]]
```

---

#### 数组转Map

```js
new Map([
	[true, 7],
	[{foo: 3}, ['abc']]
])
```

---

#### Map转对象

​	如果所有Map的键都是字符串，那它可以转为对象。

```js
function strMaptoObj(strMap) {
	let obj = Object.create(null)
	for (let [key, value] of strMap) {
		obj[key] = value
	}
	return obj
}

const map = new Map()
	.set('yes', true)
	.set('no', false);
strMaptoObj(map) // {yes: true, no: false}
```

---

#### 对象转Map

```js
function objtoStrMap(obj) {
	let map = new Map()
	for (let key of Object.keys(obj)) {
		map.set(key, obj[key])
	}
	return map
}

objtoStrMap({yes: true, no: false}) // Map(2) {"yes" => true, "no" => false}
```

---

#### Map转JSON

​	Map转为JSON要区分两种情况。一种情况是：Map的键名都是字符串，这时可以选择转为JSON对象。

```javascript
function strMaptoJson(strMap) {
	return JSON.stringify(strMaptoObj(strMap))
}

let map = new Map()
	.set('yes', true)
	.set('no', false);

strMaptoJson(map) // '{"yes":true,"no":false}'
```

​	另一种情况是，Map的键名有非字符串，这时可以选择转为数组JSON。

```javascript
function maptoArrayJson(map) {
	return JSON.stringify([...map])
}

let map = new Map()
	.set(true, 7)
	.set({foo: 3}, ['abc']);

maptoArrayJson(map) // '[[true,7],[{"foo":3},["abc"]]]'
```

---

### JSON转Map

​	JSON转为Map，正常情况下，所有键名都是字符串。

```javascript
function jsontoStrMap(jsonStr) {
	return objtoStrMap(JSON.parse(jsonStr))
}

jsontoStrMap('{"yes":true,"no":false}') // Map(2) {"yes" => true, "no" => false}
```

​	但是，有一种特殊情况，整个JSON就是一个数组，且每个数组成员本身，又是一个有两个成员的数组。这时它可以一一对应的转为Map，这往往是数组转为JSON的逆操作。

```javascript
function jsontoMap(jsonStr) {
	return new Map(JSON.parse(jsonStr))
}

jsontoMap('[[true,7],[{"foo":3},["abc"]]]') // Map(2) {true => 7, {…} => Array(1)}
```

