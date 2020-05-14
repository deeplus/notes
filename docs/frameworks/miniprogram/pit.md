# 小程序中的坑

### 2.1 事件传参

​	小程序里面只能绑定函数名称，不能进行传参；如果传参，小程序会把函数名连同参数一起当作函数名，虽然不会报错，但是会被警告；如果需要传参，可以通过自定义数据

```html
<!-- sayName('hello')会被当作是一个函数名 -->
<view bindtap="sayName('hello')"></view>
```

```html
<!-- 曲线救国 -->
<view bindtap="sayName" data-msg="hello"></view>
```

---

### 2.2 页面和页面之间传参

​	小程序并没有给我们提供一个类似 vuex 的存在，让我们能够去管理一些全局的状态和信息。为了解决该问题，通常的做法是在 app.js 中定义全局的数据，然后在所有的子页面中都能去调用

```js
// app.js
APP({
	Global_Data: {
		name: "alice"
	},
    sayHello(){
        console.log('hello')
    }
})
```

```js
// index.js
const app = getApp()
Page({
    app.Global_Data.name // 获取全局数据
    app.sayHello // 获取全局方法
})
```

---

### 2.3 状态栏

​	小程序状态栏的文字颜色只能是 `black`或 `white`，状态栏的背景色只能使用 `十六进制`。在配色的选择上，深色调用白色文字，浅色调用黑色文字，避免使用红绿色盲看不清的颜色。

---

### 2.4 根路径

​	`/` 在各个文件中的表现形式不一致：在 wxml 和 wxss 中输入 `/` 是从当前项目根目录出发 ；在 js 中输入 `/` 会从该项目所在盘符的根目录出发 ( 而在 wx.navigateTo中设置 url 时，`/` 又是从当前项目的根目录出发 )

---

### 2.5 image

​	如下，当我们引入一张图片的时候，图片往往会变形，这是因为 image 元素有默认设置的 width 和 height ，如果在引入图片时没有手动去设置 width/height， 图片没法自适应。

```html
<image src="/source/images/user.png"></image>
```

---

### 2.6 背景图片

​	 小程序的标签里边可以允许使用本地图片，但是背景图片只允许使用`在线图片`或者 `base64`

---

### 2.7 页面层级

​	小程序的页面跳转逻辑是有一定上限的，最多不能超过 `9` 次，但从业务逻辑来说，页面的嵌套最好是 `5` 层以下。

---

### 2.8 数据响应系统

​	我们通过 this.data.msg = 'newValue' 这样的方式去修改 data 中的数据时，从调试工具能够看到 appData 的数据其实已经改变了，但是却没有响应到视图，这说明：小程序并不是使用类似 proxy 或者 definedProperty 的方式从底层上做的数据监听。要想实现数据的响应，只能使用小程序提供的 api。

```js
this.setData({
    msg: "newValue"
})
```

