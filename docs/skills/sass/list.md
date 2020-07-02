# 列表

### 列表函数 -- length

返回列表长度

```bash
length(5px 10px) => 2

length(5px 10px 5px 0) => 4
```

### 列表函数 -- nth

返回列表指定索引的项目

```bash
nth(5px 10px, 2) => 10px
```

### 列表函数 -- index

返回指定项目的索引

```bash
index(1px solid red, solid) => 2
```

### 列表函数 -- append

向列表中添加新的项目

```bash
append(5px 10px, 5px) => (5px 10px 5px)
```

### 列表函数 -- join

合并列表

```bash
# 第三个参数用于指定分隔符
join(5px 10px, 5px 0, comma) => (5px, 10px, 5px, 0)
```







