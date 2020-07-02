# import



### @import

​	css本身带了一个导入的功能，在一个css文件里面我们可以把其它的css导入进来。但是每次使用 @import 浏览器都会发出新的http的请求，去下载被导入的 css文件，而每次http请求都会消耗服务器的部分资源，这样就会让页面变得更慢一些。

​	sass拓展了import的功能，可以让我们在一个scss文件中将其它的scss文件包含进来，最终scss会把它们编译为一个css文件，这样我们就可以把一个项目需要的样式分割成不同的小的部分，然后用import的方式将这些小部分的样式包含到一个css文件中，这些小的部分在sass中被称为 partials ，每一个partials 就是一个 sass文件，文件的命名需要以 `_` 开头 ，这样sass就能够把该文件识别为一个partials，就不会去单独编译改文件。

​	partials能够让css项目模块化，并且更有条理性。

### partials

#### 定义文件时，通过 _ 将该文件标示为partials

```scss
/* _base.scss */ 
body {
    margin: 0;
    padding: 0;
}
```

#### 导入文件时，不需要 _ 

```scss
/* style.scss */ 
@import "base"; /* 导入_base.scss */

.alert {
    padding: 15px;
    a {
        font-weight: bold;
    }
}

.alert-info {
    @extend .alert;
    background-color: #d9edf7;
}
```

---

```css
/* 编译输出 */
body {
    margin: 0;
    padding: 0;
}

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

