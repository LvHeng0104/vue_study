## 九.组件基础
### 9.1 特点

- 组件分为全局式和局部式的 使用`Vue.component`创建的组件都是全局的
- 组件是可重复的
- 组件的data必须是一个函数,因此,每个组件都可以维护其独自的一份数据,否则相同组件不同个体之间会造成数据冲突
- 组件只能拥有一个根节点
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
			<base-component></base-component>
			<base-component></base-component>
			<base-component></base-component>
			<base-component></base-component>
			<base-component></base-component>
		</div>
	</body>
	
	<script type="text/javascript">
		Vue.component('base-component',{
			data:function(){
				return {
					count:0
				}
			},
			template:'<button v-on:click="count++">点击我{{count}}次</button>'
		})
		
		new Vue({
			el:"#app"
		})
	</script>
</html>


```


### 9.2 给组件传参
给以个组件设置props,为其留出接受数据的端口

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title>组件传参</title>
	</head>
	
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<param_com good="哈哈哈" ></param_com>
			
			<param_com v-for="post in posts" :key='post.id' :good='post.title'></param_com>
		</div>
	</body>
	
	<script type="text/javascript">
		
		Vue.component('param_com',{
			props:['good'],
			template:'<h1>{{good}}</h1>'
		})
		
		new Vue({
			el:"#app",
			data:{
				 posts: [
				      { id: 1, title: 'My journey with Vue' },
				      { id: 2, title: 'Blogging with Vue' },
				      { id: 3, title: 'Why Vue is so fun' }
				    ]
			}
		})
	</script>
</html>

```




