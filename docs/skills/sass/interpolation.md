# interpolation

### 介绍

interpolation可以让我们把一个值插入到另一个值里边，在sass里边，interpolation可以用这样的形式把变量或表达式放到一组带#的花括号里面。使用interpolation的语法，我们可以在样式的表达式或属性上使用变量或表达式。

### 在注释中插入变量

```scss
$version: "0.0.1";
/* 项目当前的版本是：#{$version} */
```
---
编译输出：
```css
/* 项目当前的版本是：0.0.1 */
```

### 在css选择器中插入变量

想要在选择器中使用变量，直接这样写是不行的：

```scss
$name: "info";

.alert-$name {
    color: red;
}
```

---

正确的做法：

```scss
.alert-#{$name} {
    color: red;
}
```

---

编译输出：

```css
.alert-info {
    color: red;
}
```
### 在css属性中插入变量

```scss
$attr: "border";

.alert {
    #{$attr}-color: #ccc;
}
```

---

编译输出：

```css
.alert {
    border-color: #ccc;
}
```



