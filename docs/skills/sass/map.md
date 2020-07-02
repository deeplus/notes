# map

### map数据

```scss
$map: (key1: value1, key2: value2, key3: value3)
```

```bash
$color: (light: #fff, dark: #000)
```

### map函数 -- length

```bash
length($color) => 2
```

### map函数 -- map-get

```bash
map-get($color, light) => #fff
```

### map函数 -- map-keys

```bash
map-keys($color) => ("light", "dark")
```

### map函数 -- map-values

```bash
map-values($color) => (#fff, #000)
```

### map函数 -- map-has-key

```bash
 map-has-key($color, light) => true
```

### map函数 -- map-merge

```bash
$colors: map-merge($color, light-gray: #e5e5e5) => (light: #fff, dark: #000, light-gray: #e5e5e5)
```

### map函数 -- map-remove

```bash
map-remove($colors, light, dark) => (light-gray: #e5e5e5)
```





