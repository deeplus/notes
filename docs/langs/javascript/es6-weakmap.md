# WeakMap

​	**`WeakMap`**对象是一组键/值对的集合，其中的键是弱引用的，其键必须是对象，而值可以是任意的。WeakMap与Map结构类似，也是用于生成键值对的集合。WeakMap与Map的区别有两点：

* WeakMap只接收对象作为键名（null除外），不接受其它类型的值作为键名。
* WeakMap键名所指的对象，不计入垃圾回收机制。

---

### WeakMap的用途

​	WeakMap设计的目的在于，有时我们想在某个对象上面存放一些数据，但是这会形成对于这个对象的引用。

```javascript
const e1 = document.getElementById('foo')
const e2 = document.getElementById('bar')
const arr = [
	[e1, 'foo元素'],
	[e2, 'bar元素']
]
/*
*	e1,e2是两个对象，我们通过arr数组对这两个对象添加一些文字说明，这就形成了arr对e1，e2的引用
*	一旦不再需要这两个对象，我们就必须手动删除这个引用，否则垃圾回收机制就不会释放e1，e2所占用的内存
*/ 
```

​	Map就是为了解决这个问题而诞生的，它的键名所引用的对象都是弱引用，即垃圾回收机制不将该对象的引用考虑在内。

```javascript
const wm = new WeakMap()
const element = document.getElementById('example')

wm.set(element, 'some informations')
wm.get(element) // 'some informations'
```
