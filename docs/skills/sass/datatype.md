# 数据类型

### 类型

sass支持6种主要的数据类型：

*    数字 : 1, 2, 13, 10px
*    字符串 : 有引号字符串与无引号字符串，"foo", "bar", baz
*    颜色 : blue, #04a3f9, rgba(255, 0, 0, .5)
*    布尔型 : true, false
*    空值 : null
*    数组(list) : 用空格或逗号作分隔符, 1.5em 1em 0 2em, Helvetica, Arial, sans-serif
*    maps : 相当于 JavaScript 的 object，(key1: value1, key2: value2)

### 类型监测

```bash
$ sass -i

$ type-of(#04a3f9) // 'color'
$ type-of(1px solid #ccc) // 'list'
```

