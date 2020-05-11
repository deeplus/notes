# String拓展

​	es2017 引入了字符串补全长度的功能，如果某个字符串不够指定长度，则会在头部或尾部补全。

### padStart()

​	用另一个字符串填充当前字符串的头部，以便产生的字符串达到给定的长度。

> 语法：
>
> ```javascript
> str.padStart(targetLength[, padString])
> ```
>
> 参数：
>
> * **`targetLength`**：当前字符串需要填充到的目标长度；
>
> * **`padString`**：填充字符串。

* 如果原字符串的长度，大于或等于指定的最小长度，则返回原字符串；
* 如果用来补全的字符串和原字符串，两者的长度之和超过了指定的最小长度，则会截去超出部分的补全字符串；
* 如果省略第二个参数，默认使用**`空格(U+0020)`**补全长度。

```javascript
'abc'.padStart(10) // '       abc'
'abc'.padStart(10, 'foo') // 'foofoofabc'
'abc'.padStart(6, '123456') // '123abc'
'abc'.padStart(8, '0') // '00000abc'
'abc'.padStart(1) // 'abc'
```

---

### padEnd()

​	用一个字符串填充当前字符串的尾部，返回填充后达到指定长度的字符串。

> 语法：
>
> ```javascript
> str.padEnd(targetLength[, padString])
> ```
>

```javascript
'abc'.padEnd(10) // 'abc       '
'abc'.padEnd(10, 'foo') // 'abcfoofoof'
'abc'.padEnd(6, '123456') // 'abc123'
'abc'.padEnd(1) // 'abc'
```



