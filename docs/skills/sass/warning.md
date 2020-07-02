# 警告与错误

### 介绍

​	在我们自己设计的函数或者 mixin 里面，可以包含一些警告或者错误的提示信息 ... 这样用户在错误的使用你的函数或者 mixin 的时候，可以看到这些提醒 ...

​	显示警告信息，可以使用 @warn 这个指令，显示错误信息，用的是 @error ... 

### 示例

```scss
$colors: (light: #fff, dark: #000);

@function color($key) {
    @if not map-has-key($colors, $key) {
        @error "在 $colors 里没有找到 #{$key} 这个 key";
    }
    
    @return map-get($colors, $key);
}

body {
    background-color: color(gray);
}
```

### 编译输出

```css
/* Error: "在 $colors 里没有找到 gray 这个 key"
 *    ,
 * 12 |     background-color: color(gray);
 *    |                       ^^^^^^^^^^^
 *    '
 *   style.scss 12:23  root stylesheet */
```

