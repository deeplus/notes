# 进程通信

### 进程间通信的目的

*    通知事件
*    数据传输
*    共享数据

---

### IPC模块通信

*    electron提供了 IPC 通信模块，主进程的 ipcMain 和渲染进程的 ipcRenderer
*    ipcMain 和 ipcRenderer 都是 EventEmitter 对象

---

### 渲染进程到主进程

*    callback写法：
    *    ipcRenderer.send(channel, ...args)
    *    ipcMain.on(channel, handler)

*    Promise写法 (electron 7.0 之后，处理请求 + 响应模式)：
    *    ipcRenderer.invoke(channel, ...args)
    *    ipcMain.handle(channel, handler)



*    示例

```js
// main.js
let win
app.on('ready', () => {
    win = new BrowserWindow({
        width: 300,
        height: 300,
        webPreferences: {
            nodeIntegration: true
        }
    })
    win.loadFile('./index.html')
    handleIPC()
})

function handleIPC() {
    ipcMain.on('do-some-work', function(e, a, b) {
        console.log('do-some-work', a, b)
    })
}
```

```js
// renderer.js
const {ipcRenderer} = require('electron')

ipcRenderer.send('do-some-work', 1, 2)
```

---

### 主进程到渲染进程

​	从主进程发送事件到渲染进程 => 需要考虑到底是发送给哪个窗口

*    callback写法：
    *    ipcRenderer.on(channel, handler)
    *    webContents.send(channel)

```js
// main.js
const {app, BrowserWindow, ipcMain} = require('electron')

let win
app.on('ready', () => {
    win = new BrowserWindow({
        width: 300,
        height: 300,
        webPreferences: {
            nodeIntegration: true
        }
    })
    win.loadFile('./index.html')
    setTimeout(handleIPC, 500)
})

function handleIPC() {
    win.webContents.send('do-some-render-work')
}
```

```js
// renderer.js
const {ipcRenderer} = require('electron')

ipcRenderer.on('do-some-render-work', () => {
    console.log('do some work')
})
```

---

### 渲染进程到渲染进程（页面间）

*    通知事件
    *    通过主进程转发（electron 5之前）
    *    ipcRenderer.sendTo（electron 5之后）
*    数据共享
    *    web技术（localStorage、sessionStorage、indexedDB）
    *    使用 remote（不建议）

```js
// main.js
let win, win2
app.on('ready', () => {
    win = new BrowserWindow({
        width: 300,
        height: 300,
        webPreferences: {
            nodeIntegration: true
        }
    })
    win.loadFile('./index.html')

    win2 = new BrowserWindow({
        width: 300,
        height: 300,
        webPreferences: {
            nodeIntegration: true
        }
    })
    win2.loadFile('./index2.html')
    global.sharedObject = {
        win2WebContentsId: win2.webContents.id
    }
})
```

```js
// renderer.js
const {ipcRenderer, remote} = require('electron')

let sharedObject = remote.getGlobal('sharedObject')
let win2WebContentsId = sharedObject.win2WebContentsId

ipcRenderer.sendTo(win2WebContentsId, 'do-some-work', 1)
```

```js
// renderer2.js
const {ipcRenderer} = require('electron')

ipcRenderer.on('do-some-work', (e, a) => {
    alert('renderer2 handle some work' + a)
})
```

---

### 经验&技巧

*    少用 remote 模块
    *    每次 remote 都会触发底层的同步 ipc 事件，特别影响性能，如果 remote 处理的不好，甚至会导致整个应用卡死
*    不要用 sync 模式
*    在请求 + 响应的通信模式下，需要自定义超时限制

