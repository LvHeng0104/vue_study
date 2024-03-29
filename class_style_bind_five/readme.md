# 绑定Class和Style

  * [五.绑定Class和Style](#五绑定class和style)
    * [5.1 对象语法](#51-对象语法)
  * [5.2 Class绑定语法使用计算属性](#52-class绑定语法使用计算属性)
  * [5.3 数组语法](#53-数组语法)
    * [5.4 行内样式绑定](#54-行内样式绑定)


## 五.绑定Class和Style
### 5.1 对象语法
> 给`:class`一个对象,可动态切换clss
> 
> 绑定一个Class 首先需要该CSS存在
>
> 绑定语法可以决定是否使用该CSS

```HTML

<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title></title>
	</head>

	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<style type="text/css">
		.static {
			width: 12.5rem;
			height: 12.5rem;
			background-color: lightblue;
		}

		.class1 {
			background-color: lightgoldenrodyellow;
		}
		.class2{
			background-color: red;
		}
	</style>
	<body>
		<div id="app">
			<!-- 不需要动态绑定的直接引入 -->
			<div class="static">
				a
			</div>
			<hr />
			<button @click="changehasError">点击修改hasError的值</button>
			<div class="static" :class="{class1:isActive,class2:hasError}">
				b
			</div>
		</div>
	</body>

	<script type="text/javascript">
		let vm = new Vue({
			el: "#app",
			data: {
			 isActive: true,
			  hasError: false
			},
			methods:{
				changehasError(){
					this.hasError = !this.hasError
				}
			}
		})
	</script>
</html>

```

## 5.2 Class绑定语法使用计算属性
```HTML
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title></title>
	</head>
		<style type="text/css">
		.static {
			width: 12.5rem;
			height: 12.5rem;
			background-color: lightblue;
		}
	
		.class1 {
			background-color: lightgoldenrodyellow;
		}
		.class2{
			background-color: red;
		}
	</style>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<!-- 不需要动态绑定的直接引入 -->
			<div class="static" :class="ClassObject">
				a
			</div>

		</div>
	</body>
	
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				
			},
			computed:{
				ClassObject:function(){
					return {
						class1:true
					}
				}
			}
		})
	</script>
</html>

```


## 5.3 数组语法
> 给 `:class`传递一个数组,应用一个样式列表

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title></title>
	</head>
	<style type="text/css">
		.static {
			width: 12.5rem;
			height: 12.5rem;
			background-color: lightblue;
		}

		.class1 {
			background-color: lightgoldenrodyellow;
		}

		.class2 {
			background-color: red;
		}
	</style>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<!-- 通过isActive的属性值来判定是否添加class1样式 -->
			<div  :class="[staticObject,isActive?classObject:'']">
				a
			</div>
			
			<hr>
			<!-- 同样,上面的表达式也可以使用对象语法 -->
			<div  :class="[staticObject,{classObject:isActive}]">
				a
			</div>
		</div>
	</body>

	<script type="text/javascript">
		let vm = new Vue({
			el: "#app",
			data: {
				isActive:true,
				classObject:"class1",
				staticObject:"static"
			}
		})
	</script>
</html>

```





### 5.4 行内样式绑定
> 基本上和Class绑定的通用,但是有一些问题需要注意,详将如下

```HTML
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
			<!-- 单个样式绑定 -->
			<div :style="{color:activeColor,fontSize:activeFont}">a</div>
			<hr >
			<!-- 绑定一组样式,有些样式不支持,比如background-color-->
			<div :style="styleObject">b</div>
			
		
			
			
			
		</div>
	</body>

	<script type="text/javascript">
		new Vue({
			el: "#app",
			data: {
				activeColor:"red",
				activeFont:"20px",
				styleObject:{
					width: "12.5rem",
					height: "12.5rem",
					/* vue应该是有bug,没办法识别 -  */
					// background-color: "lightgoldenrodyellow",
					// font-style: oblique,
					color:"yellow"
				}
			}
		})
	</script>
</html>

```
