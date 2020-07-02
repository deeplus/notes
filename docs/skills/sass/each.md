# @each

### 介绍

@each 指令用于根据列表内的项目去生成特定的样式

### 语法

```scss
@each $var in $list {
    ...
}
```

### 示例

```scss
$icons: success error warning;

@each $icon in $icons {
    .icon-#{$icon} {
        background-image: url(../images/icons/#{$icon}.png)
    }
}
```

### 编译输出

```css
.icon-success {
    background-image: url(../images/icons/success.png);
}

.icon-error {
    background-image: url(../images/icons/error.png);
}

.icon-warning {
    background-image: url(../images/icons/warning.png);
}
```

