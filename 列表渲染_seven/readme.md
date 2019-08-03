## 七.列表渲染
### 7.1 列表渲染语法
```html
	<ul id="example-1">
	  <li v-for="item in items">
		{{ item.message }}
	  </li>
	</ul>
```

```js
	var example1 = new Vue({
	  el: '#example-1',
	  data: {
		items: [
		  { message: 'Foo' },
		  { message: 'Bar' }
		]
	  }
	})
```


### 7.2 for中的下标 和 遍历对象 
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
			<h5>给每个列表子项绑定一个key,用于重新渲染一个新的列表</h5>
			<li v-for="(item,index) in items" key='index'>
				<!-- 在v-for中,可以访问所有的父作用域属性 -->
				{{parentMessage}} - {{index}} - {{item.message}} 
			</li>
			<hr>
			<br>
			<h4>读取对象的所有value</h4>
			<!-- 遍历对象,会读取该对象的所有属性-->
			<li v-for="ob in obj">
				{{ob}}
			</li>
			<h4>读取对象的所有 k - v</h4>
			<!-- 也可以读取key -->
			<li v-for="(value,key) in obj">
				{{key}}:{{value}}
			</li>
		</div>
	</body>

	<script type="text/javascript">
		new Vue({
			el: "#app",
			data: {
				parentMessage: 'Parent',
				items: [{
						message: 'Foo'
					},
					{
						message: 'Bar'
					}

				],
				obj: {
					name: '张三',
					age: '18',
					address: '南京'
				}
			}
		})
	</script>
</html>

```


### 7.3 变异方法
> 变异方法用于数组元素更新时,DOM上渲染的数组会被响应式的重新渲染

> 这些被Vue重新定义的方法,除了其拥有的响应式特性之外,他们不会创建新的数组,而是修改原本的数组

> 变异方法: 数组因某个方法导致的局部变更
- `push()` : 向数组的末位添加一个或多个元素,并返回新的长度.
- `pop()` : 删除,并返回数组的最后一个元素
- `shift() `: 删除,并返回数组的第一个元素
- `unshift()` : 向数组的开头添加一个或者多个元素,并返回新的长度
- `splice()` : 删除一个元素,并向数组添加新的元素
- `sort()` : 对数组进行排序
- `reverse()` : 颠倒数组中的元素顺序


### 7.4 替换数组
> 替换数组: 数组因为某些方法导致从内存地址上的整体变更
- filter(Function) :  过滤,通过其中函数参数来进行过滤,并返回一个新的数组
- concat() : 截取并连接,可以将两个或多个数组中的某一段元素进行重新连接,生成一个新的数组,但不会改变原有数组
- slice() : 从一个数组中返回特定位置的元素,就像是截取字符串那样

这些方法也是响应式的,并且vue不会重新渲染整个DOM,而是替换其中的某些元素




### 7.5 不支持响应式的变更模式
1. 使用索引直接设置一个数组元素时:
> `vm.items[index] = newValue`

2. 修改数组的长度时
> `vm.items.length = newLength`

	```js
	var vm = new Vue({
	  data: {
		items: ['a', 'b', 'c']
	  }
	})
	vm.items[1] = 'x' // 不是响应性的
	vm.items.length = 2 // 不是响应性的
```

#### 解决方案
Vue实例本身提供了一个全局方法 `Vue.set` 也可简写为 $vm.set
```javascript
	Vue.set(vm.array,indexOfitems,newValue)
```

若是要解决第更换长度的问题
```javascript
	vm.array.splice(newLength)
```
