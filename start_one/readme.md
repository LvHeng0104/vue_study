# Table of Contents

  * [一.起步](#一起步)
    * [1.1 vue是响应式的](#11-vue是响应式的)
    * [1.2 绑定vue成员变量到dom属性](#12-绑定vue成员变量到dom属性)
    * [1.3 条件](#13-条件)
    * [1.4 遍历循环](#14-遍历循环)
    * [1.5 事件监听器](#15-事件监听器)
    * [1.6 即时数据渲染](#16-即时数据渲染)
    * [1.7 组件](#17-组件)
      * [1.7.1 非动态组件](#171-非动态组件)
      * [1.7.2 动态参数绑定](#172-动态参数绑定)




> 2019-7-23 vue学习仓库创建,该文件用于记录笔记


## 一.起步
### 1.1 vue是响应式的
```javascrip

	<!DOCTYPE html>
	<html>
		<head>
			<meta charset="utf-8">
			<title></title>
		</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
		<body>
			<div id="app">
				{{message}}
			</div>
		</body>
		
		<script type="text/javascript">
			var app = new Vue({
				<!-- el:定义要被vue渲染的dom容器  -->
				el:"#app",
				<!-- data:vue对象全局可使用的参数 -->
				data:{
					message:"hello vue"
				}
			})
		</script>
	</html>
		<!-- 参数即时修改，前端及时响应变更 -->

```


### 1.2 绑定vue成员变量到dom属性

> v-bind 是绑定指令, 所有以 v- 为前缀的都是指令
>  
> **他们会在DOM上渲染特殊的 `响应式行为`(数据变化时可自动更新数据)**


```javascript
<!DOCTYPE html>
<html>
<head>
	<title></title>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
	
</head>
	<body>
		<div id="app">
			<!-- 这段组合代码作用是在文字上鼠标悬浮展示message的值 -->
			<!-- 其中 v-bind 可以省略,直接通过title="message"的方式可以达到同样的效果 -->
			<span v-bind:title="message">
				鼠标悬浮展示
			</span>
		</div>
	</body>
	<script type="text/javascript">
		var app = new Vue({
			el:"#app",
			data:{
				message:"hello vue"
			}
		});
		
	</script>
</html>
```

### 1.3 条件
```JavaScript
<!DOCTYPE html>
<html>
	<head>
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
	<body>
		<div id="app">
			<button type="button" @click="turn">开关</button>
			<!-- if中的条件为Boolean类型,和js中的if()相同 -->
			<span v-if="seen">看到我了吗</span>
		</div>
	</body>
	
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				seen:false
			},
			methods:{
				turn(){
					this.seen = this.seen?false:true;
				}
			}
		})
	</script>
</html>
```


### 1.4 遍历循环


```javascript
<!DOCTYPE html>
<html>
	<head>
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
			<div id="app">
				<!-- 遍历个数,每有一个元素就会有一组<li>生成 -->
				<li v-for="item in items">
					<!-- 元素中,可使用当前遍历位置对象的属性 -->
					{{item.text}}
				</li>
			</div>
	</body>
	<script type="text/javascript">
		 new Vue({
			el:"#app",
			data:{
				items:[
					{text:"笔记记录"},
					{text:"github"},
					{text:"xiancaixifan"}
				]
			}
		})
	</script>
</html>
```


### 1.5 事件监听器
> v-on 为DOM渲染响应式的事件
> 
> v-bind,为DOM属性绑定Vue属性,v-on是为DOM事件赋值一个Vue函数

```javascript
<!DOCTYPE html>
<html>
	<head>
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<p>{{message}}</p>
			<button v-on:click="reverseMessage">吃吧</button>
		</div>
	</body>
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				message:"Xian Cai Xi Fan 好吃哦"
			},
			methods:{
				    reverseMessage() {
						this.message = this.message.split('').reverse().join('');
					}
			}
		})
	</script>
</html>
```



### 1.6 即时数据渲染
```javascript
<!DOCTYPE html>
<html>
	<head>
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<!-- 文本框中输入任意数据,下方立刻动态渲染改动数据 -->
			<input type="text" v-model="message">
			<br>
			{{message}}
		</div>
	</body>
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				message:""
			}
		})
	</script>
</html>
```

### 1.7 组件
#### 1.7.1 非动态组件

```javascript
<!DOCTYPE html>
<html>
	<head>
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
	<body>
		<div id="app">
			<ol>
				<todo-item v-for="obj in lists" v-bind:title="obj.id">
					{{obj.item}}
				</todo-item>
			</ol>
		</div>
	</body>
	<script type="text/javascript">
		
	Vue.component('todo-item', {
		<!-- 组件元素内部的信息为定死的,不许要修改, -->
		template: '<li>这是个待办项</li>'
	})
		
		var app = new Vue({
			el:"#app",
			data:{
				
				lists:[
					{id:1,item:"第一个参数"},
					{id:2,item:"第二个参数"},
					{id:3,item:"第三个参数"},
					{id:4,item:"第四个参数"},
					{id:5,item:"第五个参数"},
					{id:6,item:"第六个参数"},
				]
			}
		})
	</script>
</html>
```


#### 1.7.2 动态参数绑定
```JavaScript
<!DOCTYPE html>
<html>
	<head>
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
	<body>
		<div id="app">
			<ol>
				<todo-item 
				v-for="obj in lists" 
				v-bind:param="obj"
				v-bind:key="obj.id"
				v-bind:title="obj.id"></todo-item>
			</ol>
		</div>
	</body>
	<script type="text/javascript">
		<!-- 在组件中定义好参数的,在元素中将Vue对象中的属性传递到组件参数中,
		实现动态生成 -->
		<!-- 类似于一种函数,调用方法的传参 -->
	Vue.component('todo-item', {
		props:["param"],
		template: '<li>{{param.item}}</li>'
	})
		
		var app = new Vue({
			el:"#app",
			data:{
				lists:[
					{id:1,item:"第一个参数"},
					{id:2,item:"第二个参数"},
					{id:3,item:"第三个参数"},
					{id:4,item:"第四个参数"},
					{id:5,item:"第五个参数"},
					{id:6,item:"第六个参数"},
				]
			}
		})
	</script>
</html>
```




> 总结:使用到的指令
- v-bind 为DOM的属性动态渲染值
- v-if   判定条件
- v-for  遍历Vue中属性
- v-on   为DOM标签的事件绑定Vue函数
- v-model 为DOM即时渲染数据
- 组件
```javascript
Vue.component('组件名称',{
	[props:[组件参数名称]],
	templaet:"组件模板"
	})
```
