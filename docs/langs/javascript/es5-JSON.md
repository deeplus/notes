# JSON对象

​	**`JSON(全称JavaScript Object Notation，即JavaScript对象表示法)`** 是一种语法，用来序列化对象、数组、数值、字符串、布尔值和 null 。它基于 JavaScript 语法，但与之不同：**`JavaScript不是JSON，JSON也不是JavaScript`**。

​	**`JSON指的是一个对象的字符串表示法`**。

### 方法

#### JSON.stringify()

​	JSON 格式对象的**`序列化`**，将一个对象或数组转为一个JSON字符串。如果指定了 replacer 是一个函数，则可以选择性地替换值，或者如果指定了 replacer 是一个数组，则可选择性地仅包含数组指定的属性。

​		**`在序列化的过程中，如果有函数，大概率会被过滤掉`**。

> 语法：
>
> ```css
> JSON.stringify(value[, replacer[, space] ] )
> ```
>
> 参数：
>
> * **`value`** ：将要序列化成一个字符串的值，该值不能是函数；
>
> * **`replacer`** (可选)：替换条件。
>     * 如果该参数是一个函数，则在序列化过程中，被序列化的值的每个属性都会经过该函数的转换和处理；
>     * 如果该参数是一个数组，则只有包含在这个数组中的属性名才会被序列化到最终的 JSON 字符串中；
>     * 如果该参数为 null 或者未提供，则对象所有的属性都会被序列化；
>     * 如果不使用该参数，可以传入**`null`**。
>
> * **`space`** (可选)：指定缩进用的空白字符串，用于美化输出（pretty-print）；
>     * 如果参数是个数字，它代表有多少的空格；上限为10。该值若小于1，则意味着没有空格；
>     * 如果该参数为字符串（当字符串长度超过10个字母，取其前10个字母），该字符串将被作为空格；
>     * 如果该参数没有提供（或者为 null），将没有空格。
>

```javascript
// JSON.stringify()用于JSON格式对象的序列化
var obj = {
	a: 1,
	b: 2
}
JSON.stringify(obj) // '{"a":1,"b":2}'

// 自动过滤函数
var obj1 = {
	a: 1,
	b: function(){}
}
obj1 // {a: 1, b: ƒ}
JSON.stringify(obj1) // '{"a":1}'

// 可以转数组
JSON.stringify([1, 2, 3]) // '[1,2,3,4]'

JSON.stringify([1, 2, function(){}]) // '[1,2,null]'
```

---

#### JSON.parse()

​	JSON格式对象的**`反序列化`**，将一个JSON字符串转为一个JSON对象/值。

> 语法：
>
> ```css
> JSON.parse(text[, reviver])
> ```
>
> 参数：
>
> * **`text`**：要被解析成Javascript值的字符串;
>
> * **`reviver`**(可选) ：转换器, 如果传入该参数(函数)，可以用来修改解析生成的原始值，调用时机在parse函数返回之前。

```javascript
// JSON.parse()用于JSON格式对象的反序列化
var str = '{"a":1, "b":2}'

JSON.parse(str) // {a: 1, b: 2} 
```

---

#### 对象拷贝

```js
// 利用JSON.stringify()和JSON.parse()可以实现对对象的拷贝

var obj = {
	a: 1,
	b: 2
}

var new_obj = JSON.parse(JSON.stringify(obj))
obj === new_obj // false
```



​	

