# 修改编译输出的css格式

### 
```scss
//未编译样式
.box {
    width: 300px;
    height: 400px;
    &-title {
        height: 30px;
        line-height: 30px;
    }
}
```

### nested -- 嵌套

```bash
# 命令行内容
$ sass style.scss:style.css --style nested
```
---
```css
/*编译过后样式*/
.box {
    width: 300px;
    height: 400px; }
    .box-title {
        height: 30px;
        line-height: 30px; }
```

### expanded -- 扩展
```bash
# 命令行内容
$ sass style.scss:style.css --style expanded
```
---
```css
/*编译过后样式*/
.box {
    width: 300px;
    height: 400px;
}
.box-title {
    height: 30px;
    line-height: 30px;
}
```

### compact -- 紧凑
```bash
# 命令行内容
$ sass style.scss:style.css --style compact
```
---
```css
/*编译过后样式*/
.box { width: 300px; height: 400px; }
.box-title { height: 30px; line-height: 30px; }
```

### compressed -- 压缩
```bash
# 命令行内容
$ sass style.scss:style.css --style compressed
```
---
```css
/*编译过后样式*/
.box{width:300px;height:400px}.box-title{height:30px;line-height:30px}
```