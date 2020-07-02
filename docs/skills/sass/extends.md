# 继承/拓展



### 继承

```scss
.alert {
    padding: 15px;
}

.alert a {
    font-weight: bold;
}

.alert-info {
    @extend .alert;
    background-color: #d9edf7;
}
```
---

```css
/* 编译输出 */
.alert,
.alert-info {
    padding: 15px;
}

.alert a,
.alert-info a {
    font-weight: bold;
}

.alert-info {
    background-color: #d9edf7;
}
```

