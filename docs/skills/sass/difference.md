# .sass和.scss的区别

### 介绍
Sass有两种语法格式：使用scss语法格式的sass以.scss做为拓展名；使用sass语法格式的sass以.sass作为拓展名。

### .scss
```scss
/* sass 基础教程
by ninghao.net */

// 白日依山尽
// 黄河入海流

@import "base";

@mixin alert {
    color: #8a6d3b;
    background: #fcf8e3;
}

.alert-warning {
    @include alert;
}

ul {
    font-size: 15px;
    li {
        list-style: none;
    }
}
```

### .sass
```sass
/* sass 基础教程
   by ninghao.net

// 白日依山尽
   黄河入海流

@import base

=alert
    color: #8a6d4b
    background: #fcf8e3

.alert-warning
    +alert

ul
    font-size: 15px
    li
        list-style: none
```