# 嵌套

### 嵌套
```scss
.nav {
    height: 100px;
    ul {
        margin: 0;
        li {
            float: left;
            list-style: none;
            padding: 5px;
        }
    }
}
```
---
```css
/* 编译输出 */
.nav {
    height: 100px;
}

.nav ul {
    margin: 0;
}

.nav ul li {
    float: left;
    list-style: none;
    padding: 5px;
}
```

### 嵌套时调用父选择器
使用嵌套语法时，sass会把被嵌套的选择器拿出来，在前面加上一个空格，在加上父选择器；但在某些情况下，这样的解析是不正确的，比如下面的列子

#### 错误示范
```scss
    .nav {
        ul {
            a {
                display: block;
                color: #000;
                padding: 5px;
                :hover {
                    background-color: #0d2f7e;
                    color: #fff;
                }
            }
        }
    }
```
---
```css
/* 编译输出 */
.nav ul a {
    display: block;
    color: #000;
    padding: 5px;
}

.nav ul a :hover { /* 编译后a选择器和hover选择器之前存在空格 */
    background-color: #0d2f7e;
    color: #fff;
}
```

#### 正确的做法
```scss
    .nav {
        ul {
            a {
                display: block;
                color: #000;
                padding: 5px;
                &:hover {
                    background-color: #0d2f7e;
                    color: #fff;
                }
            }
        }
    }
```
---
```css
/* 编译输出 */
.nav ul a {
    display: block;
    color: #000;
    padding: 5px;
}
.nav ul a:hover {
    background-color: #0d2f7e;
    color: #fff;
}
```

### 示例2
```scss
.nav {
    height: 100px;
    ul {
        margin: 0;
        li {
            float: left;
            list-style: none;
            padding: 5px;
        }
    }
    & &-text {
        font-size: 15px;
    }
}
```
---
```css
/* 编译输出 */
.nav {
    height: 100px;
}
.nav ul {
    margin: 0;
}
.nav ul li {
    float: left;
    list-style: none;
    padding: 5px;
}
.nav .nav-text {
    font-size: 15px;
}
```

### 嵌套属性

```scss
body {
    font: {
        family: Helvetica, Arial, sans-serif;
        size: 15px;
        weight: normal;
    }
}

.nav {
    border: 1px solid #000 {
        left: 0;
        right: 0;
    }
}
```

```css
/* 编译输出 */
body {
    font-family: Helvetica, Arial, sans-serif;
    font-size: 15px;
    font-weight: normal;
}

.nav {
    border: 1px solid #000;
    border-left: 0;
    border-right: 0;
}
```

