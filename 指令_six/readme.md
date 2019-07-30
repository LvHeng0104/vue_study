# 指令总结
## 六.条件渲染
## [官方文档](https://cn.vuejs.org/v2/guide/conditional.html)
### 6.1 条件渲染有`v-if` `v-else` `v-else-if`

 `v-if`用于选择性的渲染一块内容.这块内容只会在判定为truthy(真值)的时候被渲染
和他配套使用的还有`v-else` `v-else-if`
```html
	<div v-if="type === 'A'">
	  A
	</div>
	<div v-else-if="type === 'B'">
	  B
	</div>
	<template v-else="type == 'c'">
	  <h1>Title</h1>
	  <p>Paragraph 1</p>
	  <p>Paragraph 2</p>
	</template>
	<div v-else>
	  Not A/B/C
	</div>
```

若需要一个条件渲染多个DOM,可以使用`template`,`v-if`等条件渲染语法不会渲染`template`本身


### 6.2 用key管理可复用的元素
Vue会尽可能高效的渲染元素,通常会复用已有元素而不是从头开始渲染,这样复用会让Vue的渲染变的更快

如下例子中,文本框并没有重新渲染,两种不同的登陆方式只是修改了同一个文本框的值
```html
<!DOCTYPE html>
<html lang="zh">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<meta http-equiv="X-UA-Compatible" content="ie=edge">
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
	<body>
		<div id="app">
			<template v-if="loginType === 'username'">
				<label>Username</label>
				<input id="user" placeholder="请输入您的用户名">
			</template>
			<template v-else>
				<label>Email</label>
				<input id="email" placeholder="请输入你的邮箱">
			</template>
			<button type="button" @click="changeLogin">toggle login  type</button>
			
		</div>
	</body>

	<script type="text/javascript">
		let vm = new Vue({
			el: '#app',
			data:{
				loginType:'username'
			},
			methods:{
				changeLogin(){
				this.loginType=	this.loginType=="username" ? "" : "username"
				}
			}
		});
	</script>
</html>

```

如果不需要控件的复用,需要在控件上绑定一个key,Vue通过key值来渲染重复控件
```html
<template v-if="loginType === 'username'">
				<label>Username</label>
				<input id="user" key="1" placeholder="请输入您的用户名">
			</template>
			<template v-else>
				<label>Email</label>
				<input id="email" key="2" placeholder="请输入你的邮箱">
			</template>
			<button type="button" @click="changeLogin">toggle login  type</button>
```


### 6.3 v-show 和 v-if 的不同
`v-show`也是渲染,用法和`v-if`一致,通过真值来判定是否显示元素

不同点:
- `v-if`是决定是否渲染,`v-show`本身就已经被渲染到DOM中了,它只是决定该元素的`display`属性
- `v-show`不支持`template`属性,也不支持`v-else`