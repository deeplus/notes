# @if

### 介绍

@if 这个指令可以让我们根据一些条件去运用特定的样式

### 语法

```scss
@if 条件 {
    ...
}
```

### 示例

```scss
$use-prefixes: false;
$theme: "dark";

body {
    @if $theme == dark {
        background-color: black;
    } @else if $theme == light {
        background-color: white;
    } @else {
        background-color: grey;
    }
}

.rounded {
    @if $use-prefixes {
        -webkit-border-radius: 5px;
        -moz-border-radius: 5px;
        -ms-border-radius: 5px;
        -o-border-radius: 5px;
    }
    border-radius: 5px;
}
```

### 编译输出

```css
body {
    background-color: black;
}

.rounded {
    border-radius: 5px;
}
```

