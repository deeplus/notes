# Class类

​	**`class`**在es6之前是保留字，es6中升级成了关键字，用于定义**`类`**。**`class`**和**`let`**、**`const`**一样：**`不存在变量提升`**、**`不能重复声明`**。

​	**`es5`**的面向对象写法和传统的面向对象语言（比如C++和Java）差异很大，很容易让新学习这门语言的程序员感到困惑。对此**`es6`**提供了更接近传统语言的写法，引入了class类这个概念，作为对象的模板。通过**`class`**关键字，可以定义**`类`**。

​	es6 的**`class`**可以看作是一个**`语法糖`**，它的绝大部分功能es5都可以实现，新的**`class`**写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。

---

### class

```js
// es5
function Person(name, age) {
	this.name = name
	this.age = age
}
Person.prototype = {
	constructor: Person,
    
	add: function() {},
    
	sub: function() {}
}

// es6
class Person {
    
	// 私有属性
	constructor(name, age) {
		this.name = name
	this.age = age
	}
    
	// 公有属性: constructor之外的都是公有属性
	add() {} 
    
	sub() {} // 方法之间不需要用,或;隔开
}
```

---

### constructor

​	如果在定义一个空类（不需要任何属性和方法）时，**`constructor`**构造函数可以不写，当使用**`new`**创建实例的时候，**`constructor`**会被默认添加。

```javascript
class As {
	// 此时constructor可以不写
}
const a = new As() // constructor被默认添加
```

​	如果是在子类继承父类的时候，不写**`constructor`**就会报错，这是因为**`super`**必须在子类的**`constructor`**中执行一次。

```javascript
class As {/*...*/}

class Bs extends As{
	constructor() { // 必须写
		super() // 必须调用
	}
}
```

---

### 继承

```js
// 基类
class Father {
	// 私有属性
	constructor(opt) {
		this.name = opt.name
		this.age = opt.age
	}
    
	// 公有属性
	sayName() {}
}

// 子类
class Son extends Father{
	constructor(opt) {
		super(opt) // 必须调用且在使用this之前调用
        
		// 私有属性的拓展
		this.sex = opt.sex
	}    
    
	// 公有属性的拓展
	sayAge() {}
}
```

---

### super

​	**`super`**这个关键字，既可以当作函数使用，也可以当作对象使用，在这两种情况下其用法完全不同。

* 子类必须在**`constructor`**方法中调用**`super`**方法，否则新建实例时会报错。这是因为子类没有自己的**`this`**对象，而是继承父类的**`this`**对象，然后对其进行加工，如果不调用**`super`**方法，子类就得不到**`this`**对象。
* 父类的静态方法也会被子类继承（嗯，就是这么绝望）。

```javascript
// 父类
class Father {
	constructor() {
        
	}
}

// 子类
class Son extends Father {
	constructor() {
		super() // es6要求: 子类的构造函数必须执行一次super函数
	}
}

/*
*	在上面的代码中：super虽然代表了父类Father的构造函数，但是返回的是子类Son的实例，即super内部的this指向了Son，因此这里的super()就相当于Father.prototype.constructor.call(this)
*/
```

---

#### 作为函数使用

​	**`super`**作为函数调用时，代表了父类的构造函数，此时**`super()`**只能用在子类的构造函数之中，用在其它地方就会报错。

```javascript
// 父类
class Father {
	constructor() {
        
	}
}

// 子类
class Son extends Father {
	constructor() {
		super()
	}
	say() {
		super() // 'super' keyword unexpected here
	}
}
```

---

#### 作为对象使用

​	**`super`**作为对象时，在原型方法中指向父类的原型对象，在静态方法中指向父类。

```javascript
class Father {
	play() {
		console.log('一起玩游戏吧')
	}
    
	static sleep() {
		console.log('一起睡觉吧')
	}
}

// 子类
class Son extends Father {
	constructor() {
		super() // 这里的 super 相当于 Father
	}
	// 原型方法
	say() {
		super.play() // 这里的 super 相当于 Father.prototype, 可以调用Father的原型方法
	}
	// 静态方法
	static eat() {
		super.sleep() // 这里的 super相当于 Father，可以调用Father的静态方法
	}
}
```

---

### static

​	类（class）通过 **static** 关键字定义静态方法。类相当于实例的原型，所有在类中定义的方法，都会被实例继承。如果要想一个方法不被继承，就需要在这个方法前加上**`static`**关键字，表示该方法是一个**`静态方法`**。

​	es6 明确规定：**`class内部只有静态方法，没有静态属性`**。

```javascript
class Ambition {
	constructor(){
        
	}
    
	// 静态方法
  static staticMethod() {
		return '这是一个静态方法' // 静态方法内部的 this 指向这个类
	}
}

// 静态属性，只能手动设置
Ambition.staticProp = '这是一个静态属性'
```
