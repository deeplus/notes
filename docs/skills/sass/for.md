# @for

### 介绍

@for 指令可以在限制的范围内重复输出格式，每次按要求（变量的值）对输出结果做出变动

### 语法

```scss
/* through会包含结束值 */
@for $var from <开始值> through <结束值> {
    ...
}

/* to不会包含结束值 */
@for $var from <开始值> to <结束值> {
    ...
}
```

### 示例

```scss
$columns: 6;

@for $i from 1 through $columns {
    .col-#{$i} {
        width: 100% / $columns * $i;
    }
}
```

### 编译输出

```scss
.col-1 {
    width: 16.6666666667%;
}

.col-2 {
    width: 33.3333333333%;
}

.col-3 {
    width: 50%;
}

.col-4 {
    width: 66.6666666667%;
}

.col-5 {
    width: 83.3333333333%;
}

.col-6 {
    width: 100%;
}
```

