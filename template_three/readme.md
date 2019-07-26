## 三.Vue语法特性 Vue本生的API
### 3.1 文本渲染
> `{{obj}}` , 学名 Mustache,无论何时,Vue对象中的obj参数发生了变化,对应大括号内渲染的值都会随之变化

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
	<body>
		
		<div id="app">
			
			//点击按钮自动动态渲染
			<span>{{message}}</span>
			<br>
			//只会渲染一次,后续不再改变
			<span v-once>{{message}}</span>
			<button @click="changeMessage">改变</button>
		</div>
	</body>
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				message:"动态渲染的参数",
				num : 0
			},
			methods:{
				changeMessage(){
					this.num++;
					this.message = '变化了'+this.num+'下';
				}
				
			}
			
		})
	</script>
</html>

```


### 3.2 DOM对象渲染
> `Mustache`只可渲染普通文本
> 如果要渲染DOM对象到HTML,类似append的操作,则要使用`v-html`

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<span>普通大括号渲染效果:</span>{{dom1}}<br />
			
			<span>v-html 渲染效果:</span><span v-html="dom1"></span>
		</div>
		
	</body>
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				dom1:"<a href='https://www.baidu.com'>点击进入百度</a>"
			}
			
		})
		
	</script>
</html>
```


### 3.3 动态绑定标签属性
> 动态的 可通过Vue对象来选择DOM属性 并进行配置

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<span v-bind:title="message">鼠标悬浮查看title</span>
			<br><br>
			<span v-bind:[property]="message">鼠标悬浮查看title</span>
			
		</div>
	</body>
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				message:"我是悬浮文字",
				property:"title"
			}
		})
	</script>
</html>

```

> 浏览器会默认的将标签上的属性转为小写,所以在定义property的时候要注意设置参数为小写


### 3.4 使用JavaScript 表达式

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title></title>
	</head>
	
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			数字表达式:{{number+1}}<br />
			布尔类型操作:{{isok?"yes":"no"}}<br />
			字符类型操作:{{str.split('').reverse().join('') }}
		</div>
	</body>
	
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				number:"100",
				isok:false,
				str:"旋转跳跃"
			}
		})
	</script>
</html>

```
