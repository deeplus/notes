# 进程



### 主进程

*    electron 运行 package.json 的main脚本的进程被称为主进程
*    每个应用只有一个主进程
*    管理原生GUI，典型的窗口(BrowserWindow、Tray、Dock、Menu)
*    创建渲染进程
*    控制应用生命周期(app)

---

### 渲染进程

*    展示web页面的进程被称为渲染进程
*    通过node.js、electron提供的api可以跟系统底层打交道
*    一个electron应用可以拥有多个渲染进程