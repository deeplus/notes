# @while

### 介绍

@while 这个指令可以让我们去指定一个条件，当条件为 true 的时候就会一直循环的去做一些事情

### 语法

```scss
@while 条件 {
    ...
}
```

### 示例

```scss
$i: 6;

@while $i > 0 {
    .item-#{$i} {
        width: 5px * $i;
    }
    $i: $i - 2;
}
```

### 编译输出

```css
.item-6 {
    width: 30px;
}

.item-4 {
    width: 20px;
}

.item-2 {
    width: 10px;
}
```

