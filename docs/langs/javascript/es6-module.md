# Module

​		es6的模块**`自动采用严格模式`**，不管你有没有在模块头部显示声明"use strict"。模块功能由**`import`**和**`export`**两个命令构成。**`import`**用于输入其它模块的功能，**`export`**用于输出其它模块提供的功能。

​		一个模块就是一个独立的文件。该文件内部的所有变量，外部都无法获取，如果希望外部能够读取模块内部的某个变量，就必须使用**`export`**输出该变量。

---

### export

​	有两种不同的导出方式，命名导出和默认导出。一个模块中定义**`多个命名导出`**，但是**`只允许有一个默认导出`**。

#### 输出变量

​	**`输出变量`**

> 语法：
>
> ```javascript
> export {name1, name2, nameN}
> 
> // 重命名导出
> export {variable1 as name1, variable2 as name2, ..., NameN}
> 
> // 默认导出
> export default expression
> ```
>
> 参数：
>
> * **`nameN`**：要导出的标识符（以便其他脚本通过**`import`**语句进行导入）。
> * **`expression`**：一个表达式，该表达式的值作为默认导出值。

---

#### 输出函数

> 语法：
>
> ```javascript
> export {myFunction}
> // 也可以写成
> export function [name]() {}
> 
> // 默认导出（函数）
> export default function [name]() {}
> ```

---

#### 输出类

> 语法：
>
> ```javascript
> export {myClass}
> // 也可以写成
> export class [name]{}
> 
> // 默认导出（类）
> export default class [name]{}
> ```

---

#### 重命名导出

​	正常情况下，**`export`**输出的变量就是本来的名字，但是可以使用**`as`**关键字重命名。

> 语法：
>
> ```javascript
> export {variable1 as name1, variable2 as name2, ..., nameN}
> ```

---

#### 注意

​	由于**`const`**命令规定的是对外的借口，所以必须与模块内部的变量建立一一对应关系。

```javascript
// 报错
export 1

// 报错
const a = 1
export a

// 正确写法1:
export const a = 1

// 正确写法2:
const a = 1
export {a}

// 正确写法3：
const a = 1
export {a as b}
```

​	同样的 ，**`function`**和**`class`**的输出，也必须遵循这样的写法。

```javascript
// 报错
function fn() {}
export fn

// 正确写法1:
function fn() {}
export {fn}

// 正确写法2:
export function fn() {}
```

​	**`export`**语句输出的接口，与其对应的值是动态绑定的关系。即通过该接口，可以实时访问模块内部的值。

```javascript
export var foo = 'foo'
setTimeout(() =>{
	foo = 'baz'
}, 500)

/*
*	上面的代码，输出foo的值为'foo'，500ms之后就变成了'baz'
*/
```

​		**`export`**可以出现在模块的任何位置，只要处于模块顶层就可以。如果处于块级作用域或函数作用域内，就会报错，这是因为**`export`**作用域编译期，**`import`**命令同样如此。

---

### import

​	使用**`export`**命令定义了模块对外的接口以后，其它JS文件就可以通过**`import`**命令加载这个模块。

```javascript
import {name1, name2, ..., nameN} from 'module-src'
```

---

#### 按需加载

**`import`**命令接收一对**`{}`**，里边指定要从其它模块导入的变量名。**`{}`**里边的变量名，必须与被导入模块对外接口的名称相同。

​	如果想为输出的变量重新取一个名字，**`import`**命令要使用**`as`**关键字，将输出的变量重新命名。

```javascript
import {export1 as import1} from 'module-src'
```

​	**`import`**后面的**`from`**指定模块文件的位置，可以是绝对路径，也可以是相对路径，后面的**`.js`**可以省略。

​	需要注意的是：**`import`**命令具有提升效果，会提升到整个模块的头部，首先执行。

```javascript
foo()

import {foo} from 'my_module'

/*
*	import的执行早于foo的调用。这种行为的本质是：import命令是编译阶段执行的，在代码运行之前
*/
```

​	由于**`import`**是静态执行，所以不能使用表达式和变量，这些只能在运行时才能得到结果的语法结构。

```javascript
// 报错
import {'f' + 'oo'} from 'my_module'

// 报错
let module = 'my_module'
import {'foo'} from 'my_module'

// 报错
if (x = 1) {
	import {foo} from 'module1'
} else {
	import {foo} from 'module2'
}
```

```javascript
import {foo} from 'my_module'
import {bar} from 'my_module'

// 等同于
import {foo, bar} from 'my_module'
```

---

#### 整体加载

​	**`import`**除了指定加载某个输出值，还可以使用整体加载。即使用**`*`**指定一个对象，所有输出值都加载在这个对象上面。

​	注意：模块整体加载所在的那个对象，不允许运行时改变。下面的写法都是不允许的：

```javascript
import * as circle from './circle.js'

// 下面的代码是不被允许的
circle.foo = 'hello'
circle.area = function () {}
```

---

### export default

​	使用**`import`**命令时，用户需要知道所要加载的变量名或函数名，否则无法加载。

​	为了给用户提供方便，让他们不用阅读文档就能加载模块，就要用到**`export default`**命令，为模块指定默认输出。

```javascript
// 默认导出函数 default_fun.js
export default function (){
	console.log('foo')
}

// 默认导出类 default_class.js
export default class {
	constructor(){
		this.name = 'foo'
	}
}
```

​		其它模块加载该模块时，其它模块可以为该匿名函数指定任意名字。需要注意的是：这时**`import`**命令后面，不能使用**`{}`**。

```javascript
import myFunc from './default_fun'
myFunc() // 'foo'
```

​		另外，**`export default`**命令用在非匿名函数之前，也是可以的。

```javascript
// default_func.js
export default function foo () {
	console.log('foo')
}

// 或者写成
function foo() {
	console.log('foo')
}
export default foo

// 在上面的代码中，foo函数的函数名foo在模块外部是无效的，加载的时候，视同匿名函数加载。
```

​	下面比较一下**`export default`**和**`export`**

```javascript
// 第一组
export default function crc32() { // 输出
	// ...
}

import crc32 form 'crc32' // 输入

// 第二组
export function crc32() { // 输出
	// ...
}

import {crc32} from 'crc32' // 输入


// 上面代码的两组写法：第一组使用 export default，对应的 import 语句不需要使用 {}，第二组使用 export，对应的 import 语句需要使用 {}
```

​	**`export default`**命令用于指定模块的默认输出。显然，一个模块只能有一个默认输出，因此**`export default`**命令只能使用一次。所以，**`import`**命令后面不用加**`{}`**，因为只可能唯一对应**`export default`**命令。

​	本质上，**`export default`**就是输出一个叫做**`default`**的变量或方法，然后系统允许你为它取任意名字。所以，下面的写法是有效的。

```javascript
// module.js
function add(x, y) {
	return x * y
}
export {add as default}
// 等同于 export default add

// app.js
import {default as foo} from 'modules'
// 等同于 export foo from 'modules'
```

​	正是因为**`export default`**命令其实只是输出一个叫做**`default`**的变量，所以它后面不能跟变量声明语句。

```javascript
// 正确
export var a = 1

// 正确
var a = 1
export default a

// 错误
export default var a = 1

/*
*	上面的代码中：export default a 的含义是将变量 a 的值赋值给变量 default，所以最后一种写法会报错。
*/
```

​		同样地，因为**`export default`**命令的本质是将后面的值，赋值给 default 变量，所以可以直接将一个值写在 **`export default`**后面。

```javascript
// 正确
export default 25

// 报错
export 25
```

---

### export和import的复合写法

​	如果在一个模块之中，先输入后输出一个模块，**`import`**语句可以与**`export`**语句写在一块。

```javascript
export {foo, bar} from 'my_modules'

// 等同于
import {foo, bar} from 'my_modules'
export {foo, bar}
```

​		模块的接口改名和整体输出，也可以采用这种写法。

```javascript
// 接口改名
export {foo as myFoo} from 'my_modules'

// 整体输出
export * from 'my_modules'
```





