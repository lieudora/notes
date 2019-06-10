# vue # [官网](https://cn.vuejs.org/v2/guide/index.html "vue官网")
 ## 起步 ##   重新梳理
	
1. 声明式渲染  

	 Vue.js 的核心是一个允许采用简洁的模板语法来声明式地将数据渲染进 DOM 的系统。  
	 v-bind 特性被称为指令。令被用来响应地更新 HTML 属性，其实它是支持一个单一 JavaScript 表达式 。v-bind:class  简写  :class

2.  条件与循环  

    v-if控制显隐。
	v-for 指令可以绑定数组的数据来渲染一个项目列表。
	v-on 指令添加一个事件监听器，通过它调用在 Vue 实例中定义的方法。
	v-model 指令，它能轻松实现表单输入和应用状态之间的双向绑定。

3.  组件化应用构建  
	
	1.  在 Vue 里，一个组件本质上是一个拥有预定义选项的一个 Vue 实例。在 Vue 中注册组件很简单：  
    eg:  
	   &ensp; &ensp; &ensp;js：  
	// 定义名为 todo-item 的新组件    
		`Vue.component('todo-item', {  `  
		 &ensp;&ensp;&ensp;` template: '<li>这是个待办项</li>'`    
		`})`    
	现在你可以用它构建另一个组件模板：  
	`<ol> `  
    `<!-- 创建一个 todo-item 组件的实例 --> `  
    &ensp;&ensp;&ensp;`<todo-item></todo-item>`  
    `</ol> `  
# 一 . Vue实例 #
## 创建一个Vue实例 ##

每个 Vue 应用都是通过用 Vue 函数创建一个新的 Vue 实例开始的：
	`var vm = new Vue({`
	`// 选项`
	`})`
## 数据与方法 ##
   当一个 Vue 实例被创建时，它将 data 对象中的所有的属性加入到 Vue 的响应式系统中。     
   当这些数据改变时，视图会进行重渲染。值得注意的是只有当实例被创建时 data 中存在的属性才是响应式的。  
  *这里唯一的例外是使用 Object.freeze()，这会阻止修改现有的属性，也意味着响应系统无法再追踪变化。*  
	
	除了数据属性，Vue 实例还暴露了一些有用的实例属性与方法。它们都有前缀 $，以便与用户定义的属性区分开来。
    var data = { a: 1 }
    var vm = new Vue({  
     el: '#example',  
     data: data  
     })

	vm.$data === data // => true
	vm.$el === document.getElementById('example') // => true

	// $watch 是一个实例方法
	vm.$watch('a', function (newValue, oldValue) {
  	// 这个回调将在 `vm.a` 改变后调用
	})
## 实例生命周期钩子 ##

  生命周期钩子的 this 上下文指向调用它的 Vue 实例。  
	
    注意：
	不要在选项属性或回调上使用箭头函数，比如 created: () => console.log(this.a) 或 vm.$watch
    ('a', newValue => this.myMethod())。因为箭头函数并没有 this，this 会作为变量一直向上级词法
    作用域查找，直至找到为止，经常导致 Uncaught TypeError: Cannot read property of undefined 
    或 Uncaught TypeError: this.myMethod is not a function 之类的错误。
	 
# 二 、模板语法 

Vue.js 使用了基于 HTML 的模板语法，允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据。所有 Vue.js 的模板都是合法的 HTML ，所以能被遵循规范的浏览器和 HTML 解析器解析。

在底层的实现上，Vue 将模板编译成虚拟 DOM 渲染函数。结合响应系统，Vue 能够智能地计算出最少需要重新渲染多少组件，并把 DOM 操作次数减到最少。
	
### 插值
1. 文本
  数据绑定最常见的形式就是使用“Mustache”语法 (双大括号) 的文本插值：  
    `<span>Message: {{ msg }}</span>`

2. 原始 HTML
 双大括号会将数据解释为普通文本，而非 HTML 代码。为了输出真正的 HTML，你需要使用 v-html 指令：

3. 特性  
 Mustache 语法不能作用在 HTML 特性上，遇到这种情况应该使用 v-bind 指令：
  `<div v-bind:id="dynamicId"></div>`  
如果 isButtonDisabled 的值是 null、undefined 或 false，则 disabled 特性甚至不会被包含在渲染出来的 `<button>` 元素中。

4. 使用 JavaScript 表达式  
    Vue.js 都提供了完全的 JavaScript 表达式支持。  

	 {{ number + 1 }}
	
	{{ ok ? 'YES' : 'NO' }}
	
	{{ message.split('').reverse().join('') }}
	
	<div v-bind:id="'list-' + id"></div>  

	这些表达式会在所属 Vue 实例的数据作用域下作为 JavaScript 被解析。有个限制就是，每个绑定都只能包含单个表达式，所以下面的例子都不会生效。  
    <!-- 这是语句，不是表达式 -->
	{{ var a = 1 }}
	
	<!-- 流控制也不会生效，请使用三元表达式 -->
	{{ if (ok) { return message } }}
		
		注意：
	    模板表达式都被放在沙盒中，只能访问全局变量的一个白名单，如 Math 和 Date 。你不应该在模板表
	    达式中试图访问用户定义的全局变量。
### 指令

	指令 (Directives) 是带有 v- 前缀的特殊特性。指令特性的值预期是单个 JavaScript 表达式 (v-for 是例外情况，稍后我们再讨论)。指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM。
	

1. 参数  
	一些指令能够接收一个“参数”，在指令名称之后以冒号表示。例如，v-bind 指令可以用于响应式地更新 HTML 特性：  
	<a v-bind:href="url">...</a>  
	在这里 href 是参数，告知 v-bind 指令将该元素的 href 特性与表达式 url 的值绑定。    
	另一个例子是 v-on 指令，它用于监听 DOM 事件：  
	<a v-on:click="doSomething">...</a>        		
	在这里参数是监听的事件名。我们也会更详细地讨论事件处理。
2. 动态参数

   可以用方括号括起来的 JavaScript 表达式作为一个指令的参数：
  `<a v-bind:[attributeName]="url"> ... </a>`  
	这里的 attributeName 会被作为一个 JavaScript 表达式进行动态求值，求得的值将会作为最终的参数来使用。例如，如果你的 Vue 实例有一个 data 属性 attributeName，其值为 "href"，那么这个绑定将等价于 v-bind:href。
	
	同样地，你可以使用动态参数为一个动态的事件名绑定处理函数：
	
	<a v-on:[eventName]="doSomething"> ... </a>
	同样地，当 eventName 的值为 "focus" 时，v-on:[eventName] 将等价于 v-on:focus。

3. 修饰符 (modifier)  

   是以半角句号 . 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。例如，.prevent 修饰符告诉 v-on 指令对于触发的事件调用 event.preventDefault()

### 缩写

    v-bind 缩写  

	<!-- 完整语法 -->
	<a v-bind:href="url">...</a>
	
	<!-- 缩写 -->
	<a :href="url">...</a>
	

	v-on 缩写

	<!-- 完整语法 -->
	<a v-on:click="doSomething">...</a>
	
	<!-- 缩写 -->
	<a @click="doSomething">...</a>