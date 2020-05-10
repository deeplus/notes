# vue-cli基本服务 {docsify-ignore}

### 运行指令详解

```json
"scripts": {
	"serve": "vue-cli-service serve",
	"build": "vue-cli-service build",
	"lint": "vue-cli-service lint"
}
```

---

#### vue-cli-service serve

```bash
用法：vue-cli-service serve [options] [entry]

选项：
	--open                  在服务器启动时打开浏览器
	--copy                  在服务器启动时将 URL 复制到剪切版
	--mode                  指定环境模式 (默认值：development)
	--host                  指定 host (默认值：0.0.0.0)
	--port                  指定 port (默认值：8080)
	--https                 使用 https (默认值：false)
```

​		`vue-cli-service serve` 命令会启动一个开发服务器 (基于 [webpack-dev-server](https://github.com/webpack/webpack-dev-server)) 并附带开箱即用的模块热重载 (Hot-Module-Replacement)。

​		除了通过命令行参数，你也可以使用 `vue.config.js` 里的 [devServer](https://cli.vuejs.org/zh/config/#devserver) 字段配置开发服务器。

​		命令行参数 `[entry]` 将被指定为唯一入口，而非额外的追加入口。尝试使用 `[entry]` 覆盖 `config.pages` 中的 `entry` 将可能引发错误。

---

#### vue-cli-service build

```bash
用法：vue-cli-service build [options] [entry|pattern]

选项：
	--mode                  指定环境模式 (默认值：production)
	--dest                  指定输出目录 (默认值：dist)
	--modern                面向现代浏览器带自动回退地构建应用
	--target                app | lib | wc | wc-async (默认值：app)
	--name                  库或 Web Components 模式下的名字 (默认值：package.json 中的 "name" 字段或入口文件名)
	--no-clean              在构建项目之前不清除目标目录
	--report                生成 report.html 以帮助分析包内容
	--report-json           生成 report.json 以帮助分析包内容
	--watch                 监听文件变化
```

​		`vue-cli-service build` 会在 `dist/` 目录产生一个可用于生产环境的包，带有 JS/CSS/HTML 的压缩，和为更好的缓存而做的自动的 vendor chunk splitting。它的 chunk manifest 会内联在 HTML 里。

---

### configureWebpack

​		调整 webpack 配置最简单的方式就是在 vue.config.js 中的 configureWebpack 选项提供一个对象：该对象将会被 webpack-merge 合并入最终的 webpack 配置。

```js
configureWebpack: {
	// webpack里边怎么写，这里就怎么写
	plugins: [
		new MyAwesomeWebpackPlugin()
	]
}
```

!> &emsp;&emsp;有些 webpack 选项是基于 vue.config.js 中的值设置的，所以不能直接修改。比如，你应该修改 vue.config.js 中的 outputDir 选项而不是修改 output.path；再比如：你应该修改 vue.config.js 中的 publicPath 选项而不是修改 output.publicPath；<br>
&emsp;&emsp;这样做是因为 vue.config.js 中的值会被用在配置里的多个地方，以确保所有的部分都能正常工作在一起。

​		如果需要基于环境有条件地配置行为，或者想要直接修改配置，那就换成一个函数 (该函数会在环境变量被设置之后懒执行)。该方法的第一个参数会收到已经解析好的配置。在函数内，可以直接修改配置，或者返回一个将会被合并的对象：

```js
configureWebpack: config => {
	if (process.env.NODE_ENV === "production") {
		// 为生产环境修改配置...
	} else {
		// 为开发环境修改配置...
	}
}
```

---

### webpack-chain

​		vue-cli 内部的 webpack 配置是通过 webpack-chain 维护的。这个库提供了一个 webpack 原始配置的上层抽象，使其可以定义具名的 loader 规则和具名插件，并有机会在后期进入这些规则并对它们的选项进行修改。

*    [github地址](https://github.com/neutrinojs/webpack-chain)

*    [中文文档](https://segmentfault.com/a/1190000017547171)