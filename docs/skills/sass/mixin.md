# 混合



### mixin

可以把它理解成是一块有名字的样式，可以在任何地方使用它

#### 语法

```scss
@mixin 名字 (参数1, 参数2) {
    ...
}
```

---

#### 示例

```scss
@mixin alert { /* 定义样式 */
    color: #8a6b3d;
    background-color: #fcf8e3;
    a {
        color: #664c2b;
    }
}

.alert-warning {
    @include alert; /* 使用样式 */
}
```
---
```css
/* 编译输出 */
.alert-warning {
    color: #8a6b3d;
    background-color: #fcf8e3;
}

.alert-warning a {
    color: #664c2b;
}
```

### 参数

```scss
@mixin alert($text-color, $background) {
    color: $text-color;
    background-color: $background;
    a {
        color: darken($text-color, 10%); /* 颜色加深10% */
    }
}

.alert-warning {
    @include alert(#8a6b3d, #fcf8e3); /* 传参顺序与定义顺序必须一一对应 */
}

.alert-info {
    @include alert($background:#d8edf7, $text-color:#31708f); /* 传参顺序与定义顺序不需要一一对应 */
}
```
---
```css
/* 编译输出 */
.alert-warning {
    color: #8a6b3d;
    background-color: #fcf8e3;
}

.alert-warning a {
    color: #67502d;
}

.alert-info {
    color: #31708f;
    background-color: #d8edf7;
}

.alert-info a {
    color: #245269;
}
```

