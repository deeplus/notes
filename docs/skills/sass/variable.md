# 变量

### 定义变量
Sass中使用 `$` 定义变量

```scss
$primary-color: #1269b5;
$primary-border: 1px solid $primary-color;

div.box {
    background-color: $primary-color;
}

h1.page-header {
    border: $primary-border;
}
```
---
```css
/* 编译输出 */
div.box {
    background-color: #1269b5;
}

h1.page-header {
    border: 1px solid #1269b5;
}
```