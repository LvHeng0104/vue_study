### 八. 事件处理
#### 8.1 监听事件
使用`v-on`指令将听DOM的事件,并再触发时运行一些JavaScript代码

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
			<!-- 监听事件 -->
			<button @click='item+=1'>{{item}}</button>
			<!-- 监听绑定方法 -->
			<button @click='clickMethod'>{{item}}</button>
		</div>
	</body>
	
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				item:0
			},
			methods:{
				clickMethod:function(event){
					this.item+=1
				}
			}
		})
	</script>
</html>

```


#### 8.2 事件修饰符
