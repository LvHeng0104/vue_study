# Table of Contents

  * [四.计算属性和侦听器](#四计算属性和侦听器)
    * [4.1 计算属性](#41-计算属性)
      * [4.1.2 计算属性的getter/setter](#412-计算属性的gettersetter)
    * [4.2 侦听属性](#42-侦听属性)



## 四.计算属性和侦听器

### 4.1 计算属性
> 属性计算,就是对参数进行Javscript运算

> 计算属性类似于一个funcation,和函数不同的地方在于它拥有缓存,不需要每次使用都重新计算

> 但运算在`{{}}`中使用复杂的时候,就推荐使用计算属性,将计算过程放到后台,而不是`渲染过程` 中

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
			<input type="text" v-model="message"><br>
			<span>{{message}}</span><br>
			<span>{{resersedMessage}}</span>
		</div>
	</body>
	
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				message:"信息文字"
			},
			computed:{
				//计算属性的getter
				//计算属性也算是属性,调用的时候不需要加( )
				//计算属性里面的其他属性值,就是`this.xxx`,会自动监听,一但其中数值发生变化,计算属性也会重新计算
				//如果其他属性没有变化,计算属性不会重新计算,并且一直缓存着
				resersedMessage:function(){
					//this只想当前Vue实例
					return this.message.split('').reverse().join('');
				}
			}
		})
	</script>
</html>


```


#### 4.1.2 计算属性的getter/setter

> 计算属性默认放出的是一个get接口,如例 4.1 中的代码
> 也可以手动声明一个set,其将在被指定参数被赋值后调用

> 如果使用了set,那么该侦听属性不能存在于data中进行初始化

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title>计算属性的getter和setter</title>
	</head>
	
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<button @click="messageSet">setter</button>
			<br>
			getter: <input type="text" :value="message">
			
			<br>
			
			{{target}}
		</div>
	</body>
	
	<script type="text/javascript">
		var vm = new Vue({
			el:"#app",
			data:{
				target:'q'
			},
			computed:{
				message:{
					get:function(){
						return this.target = 'message的get方法调用'
					},
					set:function(){
						return this.target = 'message的set方法调用'
					}
				}
			},
			methods:{
				messageSet(){
					this.message = '重新赋值'
				}
			}
		})
	</script>
</html>

```


### 4.2 侦听属性
> 案例中侦听了firsttitle属性,在侦听调用方法中不能给firstitle进行任何赋值,不然会造成监听死循环

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
			<input type="text" v-model="firsttitle">
			<span>{{firsttitle}}</span>
			<span>{{secondtitle}}</span>
		</div>
	</body>
	
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				firsttitle:"a",
				secondtitle:"b"
			},
			watch:{
				firsttitle:function(val){
					this.secondtitle = val + this.secondtitle;
				}
				
			},
			
		})
	</script>
</html>


```
