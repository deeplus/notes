# 用户自定义的函数

### 介绍

在sass里边，你可以把一些值传入函数中让函数进行处理，怎么样处理取决于函数本身的设计，最终函数会返回处理之后的结果。

### 语法

```scss
@function 名称 (参数1, 参数2) {
    ...
}
```

### 示例

```scss
$colors: (light: #fff, dark: #000);

@function color($key) {
    @return map-get($colors, $key);
}

body {
    background-color: color(light);
}
```

### 编译输出

```css
body {
    background-color: #fff;
}
```





