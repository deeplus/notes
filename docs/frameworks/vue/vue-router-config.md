# vue-router详解

### 2.1 多路由配置

#### 2.1.1 默认及异常情况的路由配置

```js
const routes = [
	// 默认路由配置
	{
		path: "",
		component: home
	},
	// 跳转路由
	{
		path: "/foo",
		component: foo
    },
	{
		path: "/bar",
		component: bar
    },
	// 其它路由规则无法匹配时，采用这个组件
	{
		path: "*",
		component: other
	}
]
```

!> **`*`** 匹配存在一个不太合理的效果, 我们更希望用户在输入了一个不存在的地址时实现一个地址的跳转,跳转目标是某个特殊的路由(比如error之类的)

---

#### 2.1.2 重定向

```js
const routes = [
	// 默认路由配置: 建议写在最前面
	{
		path: "",
		component: home
	},
	// 跳转路由
	{
		path: "/foo",
		component: foo
	},
	{
		path: "/bar",
		component: bar
	},
	{
		path: "/error",
		component: error
	},
	// 其它路由规则无法匹配时，则统一跳转到error组件
	{
		path: "*",
		redirect: "/error"
	}
]
```

​	对某一类路由的访问实现一个路由跳转, 这样可以更好的把用户的逻辑整理起来。

---

### 2.2 嵌套路由

```html
<div id="app">
	<p>
		<router-link to="/home">首页</router-link>
		<router-link to="/course">课程</router-link>
	</p>
	<router-view></router-view>
</div>
```

```js

```

