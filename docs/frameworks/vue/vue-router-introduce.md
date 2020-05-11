# vue-router介绍

### 什么是路由

​	这里的路由并不是指我们平时所说的硬件路由器，这里的路由就是 SPA（single page application: 单页面应用）的 `路径管理器`。vue的单页面应用是基于路由和组件的，路由用于设定访问路径，并将路径和组件映射起来。

​	传统的页面应用，是用一些超链接来实现页面切换和跳转的。在 `vue-router` 单页面应用中，则是路径之间的切换，也就是组件的切换。路由模块的本质就是建立起 url 和页面之间的`映射`关系。

​	vue 里边之所以不能使用 a 标签做跳转，这是因为用 vue 做的都是单页应用（当你的项目准备打包时，运行npm run build时，就会生成dist文件夹，这里面只有静态资源和一个index.html页面），所以你写的标签是不起作用的，你必须使用 `vue-router` 来进行管理。

​	单页面应用（SPA）的核心之一是：`更新视图而不重新请求页面`；`vue-router` 在实现单页面前端路由时，提供了两种方式：hash 模式和 history 模式，并根据 mode 参数来决定采用哪一种方式。

---

### vue-router的两种模式

#### hash模式

​	hash 模式的原理是：在 window 对象上监听 `onhashchange` 事件，监测 hash (window.location.hash) 值的变化。hash(#) 是 url 的锚点，代表的是网页中的一个位置，单单改变 # 后面的部分，浏览器只会滚动到响应的位置，不会重新加载网页；也就是说 hash 出现在 url 中，但不会被包含在 http 请求中，对后端完全没有影响，所以改变 hash 不会重新加载页面。

​	`vue-router` 默认 hash 模式 -- 使用 url 的 hash 来模拟一个完整的 url ，于是当 url 改变时，页面不会重新加载。

---

#### history模式

​	hash 模式会在 url 中自带 # ，如果不想要很丑的hash ，我们就可以使用路由的 history 模式。history 模式充分利用了html5 history 中新增的 pushState() 和 replaceState() 方法。

​	这两个方法应用于浏览器记录栈，在当前已有的 back、forward、go 的基础之上，它们提供了对历史记录修改的功能。当它们执行修改时，虽然改变了当前的 URL ，但浏览器不会立即向后端发送请求。

```js
const router = new VueRouter({
    mode: 'history',
    routes: [...]
})
```

​	当你使用 history 模式时，url 就像正常的 url，例如 `http://yoursite.com/user/id` ，也好看！不过这种模式要玩好，还`需要后台配置支持`。

---

### 声明式的导航

```html
<script src="https://cdn.bootcss.com/vue/2.6.11/vue.js"></script>
<script src="https://cdn.bootcss.com/vue-router/3.1.3/vue-router.js"></script>

<div id="app">
	<p>
		<!-- 使用 router-link 组件来导航. -->
    		<!-- 通过传入 `to` 属性指定链接. -->
    		<!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->
  			<router-link to="/foo">go to foo</router-link>
      	<router-link to="/bar">go to bar</router-link>
	</p>
  
  	<!-- 路由出口 -->
  	<!-- 路由匹配到到组件将渲染在这里 -->
  	<router-view></router-view>
</div>
```

```js
// 1. 定义路由组件
const foo = {template: `<div>foo conponent</div>`}
const bar = {template: `<div>bar conponent</div>`}

// 2. 建立路由同组件间的映射关系
const routes = [
	{path: "/foo", component: foo},
	{path: "/bar", component: bar}
]

// 3. 创建 router 实例，然后传 `routes` 配置
const router = new VueRouter({
	routes // (缩写) 相当于 routes: routes
})

// 4. 创建和挂载根实例
const app = new Vue({
	router
}).$mount("#app")
```

---

#### 自定义router-link标签

​	默认情况下，router-link 标签会被解析为 a 标签，通过 tag 属性，我们能够指定渲染后的目标标签。

```html
<router-link to="/foo" tag="span">go to foo</router-link>
<router-link to="/bar" tag="span">go to bar</router-link>
```

---

#### 自定义被激活路由元素的class名称

```js
const router = new VueRouter({
	routes,
	linkActiveClass: "layui-btn layui-btn-xs", // 默认激活的class名称："router-link-active"
	linkExactActiveClass: "router-link-exact-active" // 默认精确激活的class名称
})
```

​	可以通过该功能和 UI 框架进行融合。

---

### 编程式的导航

​	上面的方式是使用一个声明出来的固定元素实现跳转，但这种方法局限性大，必须要有某个固定的触发元素。

​	假设我们有这样一个业务场景，在一个路由组件里面点击可以切换到另一个路由组件，这时候为了实现更加柔性的跳转, 我们就引申出编程式的导航。

```html
<div id="app">
	<p>
		<router-link to="/foo">go to foo</router-link>
		<router-link to="/bar">go to bar</router-link>
	</p>
	<router-view></router-view>
</div>
```

```js
// 1. 定义路由组件
const foo = {
	template: `
		<div>foo conponent
			<button @click="goBar">go to bar</button>
		</div>
	`,
	methods: {
		goBar() {
			this.$router.push("/bar")
		}
	}
}
const bar = {
	template: `
		<div>bar conponent
			<button @click="goFoo">go to foo</button>
		</div>
	`,
  	methods: {
		goFoo() {
			this.$router.push("/foo")
		}
    }
}

// 2. 建立路由同组件间的映射关系
const routes = [
	{path: "/foo", component: foo},
	{path: "/bar", component: bar}
]

// 3. 创建 router 实例，然后传 `routes` 配置
const router = new VueRouter({
	routes // (缩写) 相当于 routes: routes
})

// 4. 创建和挂载根实例
const app = new Vue({
	router
}).$mount("#app")
```

*    this.$router.push("目标路径") ：强制跳转至某一路径；
*    this.$router.go(-1) :  返回上一级；
*    this.$router.replace("目标路径") :  路由替换。`该方法返回一个 Promise 对象 `。
