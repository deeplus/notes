# 优势

### 无兼容问题

*    不用担心在 Safari、IE 上的表现差异

*    可以大胆使用 Chrome 浏览器已经支持的 API

*    babel 中设置 targets 为 Electron 对应的 Chrome 版本

---

### 最新浏览器Feature

*    举个例子
    *    纯天然 LazyLoad (https://mathiasbynens.be/demo/image-loading-lazy)

*    https://developers.google.com/web/updates

```js
const {app, BrowserWindow} = require('electron')

let mainWindow
app.whenReady().then(() => {
    mainWindow = new BrowserWindow({
        width: 1000,
        height: 600
    })
    mainWindow.loadURL('https://mathiasbynens.be/demo/image-loading-lazy')
})
```

---

### ES6/7/8/9/10高级语法支持

*    Async await / Promise

*    String / Array / Object 等高级语法

*    BigLint

---

### 无跨域问题

*    使用 Node.js 发送请求

*    使用 Electron net 发送请求

---

### More

*    操作本地文件

*    更好用的本地 DB

*    多线程、多进程并行

