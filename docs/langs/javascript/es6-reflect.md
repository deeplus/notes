# Reflect

​	**`Reflect`**对象和**`Proxy`**对象一样，也是es6为了操作对象而提供的新API。**`Reflect`**是一个内置的对象，它提供拦截 JavaScript 操作的方法。这些方法与**`proxy handler`**的方法相同。**`Reflect`**不是一个函数对象，因此它是不可构造的。

### 设计Reflect的目的

1.   将**`Object`**对象的一些明显属于语言内部的方法（比如Object.defineProperty）放到**`Reflect`**对象上。现阶段，某些方法同时在**`Object`**和**`Reflect`**对象上部署，未来的新方法将只部署在**`Reflect`**对象上。
2.   修改某些**`Object`**方法的返回结构，让其变得更合理。比如：**`Object.defineProperty(obj, name, desc))`**在无法定义属性时，会抛出一个错误，而**`Reflect.defineProperty(obj, name, desc)`**则会返回**`false`**。
3.   让**`Object`**的操作都变成函数行为。某些**`Object`**操作是命令式，比如：**`property in obj`**和**`delete obj[property]`**，而**`Reflect.has(obj, property)`**和**`Reflect.deleteProperty(obj, property)`**让它们变成了函数行为。
4.   **`Reflect`**对象的方法与**`Proxy`**对象的方法一一对应，只要是**`Proxy`**对象的方法，就能在**`Reflect`**对象上找到对应的方法。

​	这让**`Proxy`**对象可以方便的调用对应的**`Reflect`**方法，完成默认行为，作为修改行为的基础。也就是说，不管**`Proxy`**如何修改默认行为，你总可以在**`Reflect`**上获取默认行为。	

​		

