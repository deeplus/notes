# 函数参数结尾允许逗号

​	es2017 允许函数的最后一个参数有尾逗号(trailing comma)，主要作用是方便使用git进行多人协作开发时修改同一个函数减少不必要的行变更。

​	这样的规定也使得，函数参数与数组和对象的尾逗号规则，保持一致了。

```javascript
function clownsEverywhere(
	param1,
	param2,
) {
	// ...
}

colwnsEverywhere(
	'foo',
	'bar',
)
```

