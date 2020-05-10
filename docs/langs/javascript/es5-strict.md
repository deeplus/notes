严格模式是ES5引入的，严格模式主要有以下限制：

1. 变量必须先声明再使用；

2. 函数的参数不能有同名属性，否则报错；

3. 不能使用with语句；

4. 不能对只读属性赋值，否则报错；

5. 不能使用前缀0表示八进制数，否则报错；

6. 不能删除不可删除的属性，否则报错；

7. 不能删除变量 delete prop，只能删除属性delete globe[prop]；

8. eval不会在它的外层作用域引入变量；

9. eval和arguments不能被重新赋值；

10. arguments不会自动反映函数参数的变化；

11. 不能使用arguments.callee；

12. 不能使用arguments.caller；

13. 禁止this指向全局对象；

14. 不能使用fn.caller和fn.arguments获取函数调用的堆栈；

15. 增加了保留字（比如：protected、static和interface）。

---

### 为脚本开启严格模式

​	为整个脚本开启严格模式，只需要在所有的语句之前放一个特定语句**`'use strict'`**。

```javascript
// 为整个脚本开启严格模式
'use stcict'

// code...
```

---

### 为函数开启严格模式

​	为某个函数开启严格模式，需要将**`'use strict'`**声明放在函数体的所有语句之前。

```javascript
// 为函数开启严格模式
function fn() {
	'use strict'
  
	// code...
}
```

