# Array拓展

​	es7 中Array新增了一个实例函数**`includes()`**，用来判断一个数组是否包含指定的值。

### includes()

​	用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回**`true`**，否则返回**`false`**。该方法与字符串的**`includes()`**类似，在没有该方法之前，我们通常使用数组的**`indexOf()`**方法，检测是否包含某个值。

> 语法：**`array.includes(valueToFind[, fromIndex])`**
>
> valueToFind：需要查找的元素值；
>
> fromIndex：可选，开始查找的起始位置，默认为**`0`**。如果fromIndex为负数，则表示倒数（-1表示最后一位，依次类推）。

```javascript
[1, 2, 3].includes(2) // true
[1, 2, 3].includes(2, 1) // true
[1, 2, 3].includes(2, -1) // false
```

!> **`对象数组不能使用includes()方法来检测`**；

* 如果**`fromIndex`**为正数且大于数组的长度，则会返回**`false`**，且该数组不会被搜索。

```javascript
[1, 2, 3].includes(2, 4) // false
```

* 如果**`fromIndex`**为负数且绝对值大于数组的长度，如果**`valueToFind`**存在于数组中，则返回**`true`**,否则返回**`false`**。

```javascript
[1, 2, 3].includes(3, -4) // true
[1, 2, 3].includes(4, -4) // false
```

* **`includes()`**能够区分**`NaN`**

```javascript
[1, 2, NaN].includes(NaN) // true
```
