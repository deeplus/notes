# 颜色

### 颜色函数 -- rgb与rgba

```scss
body {
    background-color: rgb(255, 255, 0);
    color: rgba(255, 255, 0, .6);
}
```

### 颜色函数 -- hsl与hsla

```scss
body {
    background-color: hsl(60, 100%, 100%); /* 色相(0~360) 饱和度(0~100%) 明度(0~100%) */
    color: hsl(60, 100%, 100%, .5);
}
```

### 颜色函数 -- adjust-hue

该函数用于调整颜色的色相值

```scss
$base-color: #ff0000;
$base-color-hsl: hsl(0, 100%, 50%);

body {
    background-color: adjust-hue($base-color-hsl, 135deg); /* #00ff48 */
    color: adjust-hue($base-color);
}
```

### 颜色函数 -- lighten与darken

该函数用于调整颜色的明度

```scss
$base-color: hsl(222, 100%, 50%); /* #004cff */
$light-color: lighten($base-color, 30%); /* #99b8ff */
$dark-color: darken($base-color, 20%); /* #002e99 */

.alert {
    border: 1px solid $base-color;
    background-color: $light-color;
    color: $dark-color;
}
```

### 颜色函数 -- saturate与desaturate

该函数用于调整颜色的纯度(饱和度)

```scss
$base-color: hsl(221, 50%, 50%);
$saturate-color: saturate($base-color, 50%);
$desaturate-color: desaturate($base-color, 30%);

.alert {
    background-color: $saturate-color; /* #0051ff */
}

.alert-info {
    background-color: $desaturate-color; /* #667699 */
}
```

### 颜色函数 -- opacify与transparentize

transparentize用于增加颜色的透明度，opacify用于增加颜色的不透明度

```scss
$base-color: hsla(222, 100$, 50%, .5);
$fade-in-color: opacify($base-color, .3);
$fade-out-color: transparentize($base-color, .2);

.alert {
    background-color: $fade-in-color; /* rgba(0, 76, 255, .8) */
    border: 1px solid $fade-out-color; /* rgba(0, 76, 255, .3) */
}
```



