# 面向对象编程

​	即**`面向对象编程思维`**。面向对象的三大特点：**`封装型`**、**`继承性`**、**`多态性`**。

### 属性

#### prototype

​	构造函数（或类）的**`prototype`**属性指向**`构造函数的 原型对象`**。

​	类的**`原型`**本质就是个JSON格式的**`对象`**，而每一层原型之间都存在相互嵌套的关系，这些嵌套关系形成了一条像铁链一样的东西，即**`原型链`**。

```css
/* Object构造函数 的原型对象 */
Object.prototype
```

---

#### \_proto_

​	实例对象的私有属性**`—proto—`**指向它的构造函数的原型对象（**`Object.prototype`**）。并且该原型对象也有一个自己的原型对象( **`_proto_`** ) ，层层向上直到一个对象的原型对象为 **`null`**。根据定义，**`null`** 没有原型，并作为这个**`原型链`**中的最后一个环节。	

```css
/* object实例对象的 构造函数的 原型对象 */
object._proto_ 
```

---

#### constructor

​	实例对象的私有属性**`constructor`**指向实例的构造函数。

```css
/* object实例对象的构造函数 */
object.construtor
```

---

### 创建一个类

```js
// 构造函数/类
function Student(name, age) {
    
	// 私有属性
	this.name = name
	this.age = age
}

// 原型方法
Student.prototype = {
    
	// 修正constructor指向: 使用'='赋值会将constructor覆盖，需要手动修正
	constructor: Student,
	eat: function(value) {
		return value
	}
}

// 静态属性
Student.info = 'nice'

// 静态方法
Student.show = function () {
	return '这是一个静态方法'
}

// 类的实例化
const student = new Student('alice', 18)
```

---

### 继承

```js
// 父类或基类
function Father(opt) {
	this.name = opt.name
	this.age = opt.age
}
Father.prototype = {
	constructor: Father,
	add: function (v) {
		return v + 1
	}
}

// 子类
function Son(opt) {
	// 继承父类的私有属性
	Father.call(this, opt)
    
	// 拓展子类的私有属性
	this.sex = opt.sex
}

// 继承父类的原型方法


/*
*@   方案1: 让子类的原型等于父类的原型：
*      Son.prototype = Father.prototype 
*      该方案由于原型是一个对象，所以是引用型数据，在对子类进行拓展的时候同样会修改父类

*@   方案2: 让父类对象成为子类对象的原型 或者说 让父类对象出现在子类对象的原型上
*     Son.prototype = new Father({})
*     该方案由于将父类的私有属性拓展到了子类的原型上，所以会导致子类的原型很奇怪

*@   方案3: 借助一个无用的第三方类，解决私有属性的问题
*     function Third() {}
*     Third.prototype = Father.ptototype
*     Son.prototype = new Third()
*     该方案在方案2的基础上完美的解决了子类的原型问题

*@   方案4: 该方案与以上三个方案毫无瓜葛
*     for (var key in Father.prototype) {
*     	Son.prototype[key] = Father.prototype[key]
*     }
*     该方案不推荐使用，因为Father.prototype.prototype无法访问，但是方案3的方法，Father自始至终都存在于Son的原型链上
*/

function Third() {}
Third.prototype = Father.prototype
Son.prototype = new Third()

// 拓展子类的原型方法
Son.prototype.sub = function(v) {
	return v - 1
}

var parson = new Son({
	name: 'alice',
	age: 18,
	sex: '女'
})
```

