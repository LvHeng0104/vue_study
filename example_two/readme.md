# Vue 实例

* [Vue实例](#vue实例)
    * [二. Vue 实例](#二-vue-实例)
      * [2.1 Vue对象的初始化](#21-vue对象的初始化)
      * [2.2 获取Vue本身的属性和方法](#22-获取vue本身的属性和方法)




### 二. Vue 实例
#### 2.1 Vue对象的初始化

> 在Vue对象初始化完成时, vm.a = 1 此时若修改datas.a的值,那么vm.a的值也会响应变化,反之亦然

> Vue对象初始化完成后,在datas中添加属性b 如:datas.b=1, Vue对象无法渲染到b, vm.b=underfine
```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
	<body>
		<div id="app">
			
		</div>
	</body>
	<script type="text/javascript">
		var datas = {a:1};
		
		// Vue实例可以直接访问data中的属性,data为其成员变量
		// vm.a = 1; 相当于 data.a
		var vm = new Vue({
			data:datas
		})
		
	</script>
</html>

```

> 上面的例子中,如果有些属性是后期将要用到的,可以现在data中初始化,
```javascript
//初始化变量,方便后期使用
	data:{
		b:"",
		a:datas.a,
		todo:[],
		isOk:false
	}
```

> Object.freeze() 冻结一个对象,使该对象无法在被修改,则Vue将无法起到响应式的作用
```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<button type="button" @click="changeMessage">改变</button>
			<input type="text" v-model="message">
		</div>
	</body>

	<script type="text/javascript">
		var datas = {
				message: "你动我试试"
			}
			
		// 点击按钮会报错,因为datas对象无法修改,是只读的
		Object.freeze(datas);
			new Vue({
				el: "#app",
				data: datas,
				methods:{
					changeMessage(){
						this.message="试试就试试"
					}
				}
			})
	</script>
</html>


```


#### 2.2 获取Vue本身的属性和方法
> Vue的实例暴露了一些有用的实例属性和方法, 用$作为前缀
