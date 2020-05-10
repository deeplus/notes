# vue-cli基本配置

### 配置文件

​		vue 的脚手架在把 webpack 隐藏之后，如果我们想要进行一些精细化的配置，可以自己在根目录下新建一个 vue.config.js 文件，然后自行配置。

```js
/* vue.config.js */
module.exports = {
		
}
```

!>	`vue.config.js 配置文件里面使用的是 vue 提供的接口，不能将 webpack 的原生配置直接拿过来用`。

---

### publicPath

​		type: "**`string`**"，default: "**`/`**"

​		默认情况下，vue-cli 会假设你的项目是被部署在一个域名的根路径上，例如：`https://www.deeplus.cn/ `；如果是被部署在一个子路径上，你就需要使用该选项指定一个子路径。

​		例如：如果你的项目是被部署在 `https://www.deeplus.cn/app/` 的目录下，你就需要进行设置：

```js
module.exports = {
	publicPath: "/app"
}
```

​		此外，该值也可以被设置为空字符串(" ")或是相对路径("./")，这样所有的资源都会被链接为相对路径，这样打出来的包可以被部署在任意路径，也可用在类似 Cordova hybrid 应用的文件系统中；

```js
module.exports = {
	publicPath: "./app"
}
```

---

### outputDir

​		type: "**`string`**"，default: "**`dist`**"

​		当运行 **`vue-cli-service build`** 时为生成的 生产环境构建文件 指定一个输出目录。注意目标目录在构建之前会被清除 (构建时传入 **`--no-clean`** 可关闭该行为)。

```js
module.exports = {
	publicPath: "./main",
	outputDir: "bundle" // 相对于 vue.config.js
}
```

---

### assetsDir

​		type: "**`string`**"，default: " "

​		为生成的静态资源文件 (js，css，font，img) 指定一个输出目录，其路径是相对于 outputDir 的。

```js
module.exports = {
	publicPath: "./main",
	outputDir: "bundle",
	assetsDir: "assets"
}
```

---

### indexPath

​		type: "**`string`**"，default: "index.html"

​		为生成的 index.html 文件指定一个输出目录，该路径是相对于 outputDir 的。

```js
module.exports = {
	publicPath: "./main",
	outputDir: "bundle",
	assetsDir: "assets",
	indexPath: "index.html"
}
```

---

### filenameHasing

​		type: "**`boolean`**"，default: "**`true`**"

​		该值的作用就是是否在生成的静态资源名称后面加上 hash 值。

```js
module.exports = {
	publicPath: "./main",
	outputDir: "bundle",
	assetsDir: "assets",
	indexPath: "index.html",
	filenameHashing: true
}
```

---

### pages

​		type: "**`object`**"，default: "undefined"

多页面打包：

​		在 multi-page 模式下构建引用，每个 page 应该有一个对应的 JavaScript 入口文件。其值应该是一个对象，对象的 key 是入口的名字，value 是：

*  一个指定了 entry，template，filename，title 和 chunks 的对象 (除了 entry 之外都是可选的)；

*  或者是一个指定了其 entry 的字符串。

```js
pages: {
	// index page
	index: {
		// 指定page的入口
		entry: "src/main.js"
    
		// 模板来源
		template: "public/index.html"
    
		// 在dist/index.html的输出
		filename: "test.html"
    
		// 在该页面中引入的包，默认情况下会包含提取出来的通用chunk和vendor chunk
		chunks: ["index"]
	}
}
```

​		**`如果我们同时在 indexPath 和 pages 里边定义了 index.html 的输出文件名，则以 indexPath 为准`**。

---

### css

​		vue-cli 里面对css的操作基本独立了出来，将各种各样的基本配置给进行了简化，这给我们的日常开发极大的减轻了负担；

```js
css: {
	// 是否将组件内部的css单独提取至一个独立的css文件中
	extract: false,
  
	// 是否为css开启source map
	sourceMap: false,

	// 向css相关的loader传递选项
	loaderOptions: {
		css: {
  		// 这里的选项会传递给css-loader
		},
		postcss: {
  		// 这里的选项会传递给css-loader
		},
 		sass: {
  		// 这里的选项会传递给css-loader
		},
		less: {
  		// 这里的选项会传递给css-loader
		},
		stylus: {
  		// 这里的选项会传递给css-loader
		}
	}
}
```

---

### devServer

​		type: "**`object`**"，default: "**`/`**"

​		所有 webpack-dev-server 的选项都支持。注意：

*  有些值像 host、port 和 https 可能会被命令行参数覆写；
*  有些值像: publicPath 和 historyApiFallback 不应该被修改，因为它们需要和开发服务器的 publicPath 同步以保障正常的工作；

​		如果你的前端应用和后端 API 服务器没有运行在同一个主机上，你需要在开发环境下将 API 请求代理到 API 服务器。这个问题可以通过 vue.config.js 中的 devServer.proxy 选项来配置:

```js
devServer: {
	proxy: "http://localhost:4000"
}
```

​	这会告诉开发服务器将任何未知请求 (没有匹配到静态文件的请求) 代理到 `http://localhost:4000`。

