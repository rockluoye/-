# vue

MVC组成：

M: Model 数据模型
V: View  视图界面
C: Controller   控制器

MVC：为了降低代码耦合度

MVVM：view《-----》ViewModel《----》Model

组件设计的原则

-页面的每个单独的可视区域/可交互区域视为一个组件

-每个组件对应一个工程目录，组件所需资源在该目录下就近维护

-页面不过是组件的容器，组件可以嵌套自由组合，形成完整的页面

```vue
<div id="app">
	{{ msg }} 
    {{ num }}   //{{}}中支持Javascript表达式的，如{{ num + 1}}
    <p v-text="msg"></p>
	<p v-html="msg"></p>
    <p v-if="isShow">v-if</p>
	<p v-show="isShow">v-isShow</p>
    <div>
        <ul>
            <li v-for="(user,index) in users">{{ user.name }}</li>
        </ul>
    </div>
    <button v-on:click="btnClick"></button>
    <button v-on:click="btnClick2"></button>
    <img v-bind:src="imgSrc" />
    <img :src="imgSrc" />   //简写方式
</div>
<script>
    new Vue({
        el:"#app",
        isShow:true,
        data:{
            msg:"hello <b>world</b>",
            num：10,
            imgSrc："logo.png",
            users：[
            {name:"aaa"},
        	{name:"bbb"},
        	]
        }，
        methods:{
            btnClick:function(){}
    		btnClick2(){this.msg = "hello"}   //简写方式,this.msg指的是data中的msg
    		
        }
    })
</script>
```

## 一，Vue组件中的渲染方法

##### 1.模板渲染

<p v-html="name"></p>为html模式识别标签

\<p v-text="name"></p>为文本模式识别标签

##### 2.控制显示隐藏

v-if=“”------直接不渲染该元素

v-show=“”--------通过display：none进行隐藏

##### 3.循环渲染列表

v-for="user  in  dict"---i为从dict中取出的元素

v-for="(user,index)  in  dict"---i为从dict中取出的元素,index为下标

##### 4.事件绑定

v-on：click=“”

\<button v-on:click="btnClick"></button>

简写方式;<button @click="btnClick2"></button>

##### 5.属性绑定

\<img v-bind:src="imgSrc" />

当数据data中的imgSrc发生改变时img中的imgSrc也会跟着改变

简写方式：\<img   :src="imgSrc" />

如：imgSrc：“https://cn.vuejs.org/images/logo.png”

##### 6.双向数据绑定

<input v-model="age"/>

随着input中的age的改变data中的age也会跟着改变

还可以：\<img   :class=‘foo：foo1’ />

若foo1为true则class为foo此时为绑定状态

foo1为false则class不为foo为解除状态，既class值为空

双向数据绑定\<input type=text v-model="username">

如：username:"xidada"

作用：改界面和数据都会变

## 二，Vue组件中的重要选项

#### 1.data数据选项------代表vue对象的数据

Vue框架会自动监视data里面的数据变化；自动更新数据到HTML标签上，自动将data中的数据进行递归转换成getter和setter，就可以自动更新了

data：{}

#### 2.computed计算属性

计算属性，既是属性也可以是方法，所以getter和setter的this上下文自动绑定为Vue的实例

\<p>商品名字：{{ name }}</p>

\<p>商品名字：{{price }}</p>

\<p>商品名字：{{ num }}</p>

\<p>商品名字：{{ total }}</p>

如：

```
computed：{
    total（）{
        return this.price * this.num
    }
}
```

#### 3.watch:监听属性的变化

argument：参数属性选项

什么是argument：这个函数体内的arguments非常特殊，实际上是所在函数的一个内置类数组对象，可以用数组的[i]和.length

有什么作用：js语法不支持重载！但可用arguments对象模拟重载效果

重载要解决的问题：

1。可变参数类型。
2。可变参数个数

arguments对象：函数对象内，自动创建的专门接收所有参数值得类数组对象

arguments[i]: 获得传入的下标为i的参数值

arguments.length: 获得传入的参数个数

callee 属性是 arguments 对象的一个成员，仅当相关函数正在执行时才可用。
callee 属性的初始值就是正被执行的 Function 对象，这允许匿名的递归函数

```
watch:{
    num：function（newVal，oldVal）{}-----与下面的是一样的
    num(newVal，oldVal){
        console.log(arguments.length)-------arguments存储传过来的实参
        if（newVal<1 || newVal>this.total）{
            newVal = oldVal；
        }	
    }
}
```

箭头函数：（n,m）=> n+m

n,m是要传的参数，n+m是要返回的结果

## 三，组件

组件：定义页面的局部区域块，完成单独的页面小功能

#### vue组件中data的写法：

```vue
export default {
    //data必须写函数
    data:function(){
        return {
        msg:"我是vue组件",
        }
    }
}
```

#### 组件demoView.vue在app.vue中的注册：

```vue
<template>
  <div id="app">
		<!-- 将组件用标签的方法导入，显示组件 -->
		<demoView></demoView>
  </div>
</template>
<script>
	//导入子组件
import demoView from './components/demoView.vue'
export default {
  name: 'app',
  components: {//注册组件
    demoView
  }
}
</script>
<style>
</style>
```

#### 父组件传参给子组件：

类似于app.vue为父组件的步骤，用属性绑定的方法给子组件传参

```vue
//会自动到子组件中获取值
<ChildView :name="name" age="age"></ChildView>
<script>
    import ChildView from './components/ChildView.vue'
	export default {
        data() {
            return{
            	name:"lisi",
            	age:22
            }
        }
	}
</script>
```

子组件中接受父组件的数据：

```vue
<script>
	export default {
        prop: [
            'name',
            'age'
        ]
	}
</script>
```

#### 子组件向父组件传参：

父组件进行事件接受操作：

```vue
<ChildView2 @recvMsg="btnClick"></ChildView>
<script>
    import ChildView2 from './components/ChildView2.vue'
	export default {
        data() {
            return{
            	msg:null
            }
        },
        methods: {
            btnClick:function(msg){
                this.msg = msg
            }
        }
	}
</script>
```

在子组件进行点击发送操作：

```vue

```

## 六，Vue路由

1.在cmd中cd到项目目录下的，执行npm install vue-router

2.在main.js中导入包----import  VueRouter from ‘vue-router’

3.在main.js使用路由Vue.use( VueRouter)

4.新建组件，在main中导入组件

5.在main.js定义路由规则

var routes = [{path:"/",redirect:某路由}，{path:"/baseview"，component:组件名称}，{.......}]

redirect重定向，设置默认页面

6.在main.js中创建路由对象

new Vue({

​	render:h => h(app),

​	routes:routes,------------------------------挂载到根vue对象

})

7.在app中使用<router-link to='/baseview'>链接</router-link>

8.在app中对组件进行渲染<router-view></router-view>

#### Axios请求：

1.cd到项目目录下，执行npm install  --save Axios

2.在main.js中导入包----import Axios from ‘axios’

3.在main.js中Vue.prototype.$ajax = Axios    -----------利用原型给所有vue对象共享属性$ajax

4.在组件中使用

```vue
create() {
    this.$ajax.get('链接')
	.then(res=>this.newArr = r.data.data.tech)
	.catch(function(e){})
}
//then为请求成功后的回掉
//catch为请求失败的回掉
```

过滤器：filters------格式化变量内容的输出

用法：<p>{{message | toupper }}</p>

\<p>{{num | topercentage }}</p>

如：filters：{

```
toupper:function(value){

	return value.toUpperCase();

},

topercentage:function(value){

	return value * 100 + '%';

},

```

}

class对象绑定：

\<div :class="myClass"></div>

data:{

```
myclass:{

	active:true,

	big:true,

}

```

}

条件渲染：v-if，v-else-if，v-else

 \<h1 v-if="result == 0">成绩未公布</h1>

\<h1 v-else-if="result <60">不及格</h1>

\<h1 v-else>{{result }}>及格</h1>

data:{

```
result:0

```

}

元素显示：v-show标记元素节点是否显示（在dom不会消失）

\<h1 v-show="result">lalalalala</h1>

data:{

```
result:true

```

},

v-model.lazy/.number/.trim

.lazy:用户输入内容时不做绑定数据的处理更新，在控件的onchange事件中更新绑定的变量

.number:将用户输入的内容转换为数值类型，若输入的为非数值型的时候，则返回NaN

.trim：自动去掉用户输入两端的空格

如：\<input type="text" id="username" v-model.lazy="username" @change="checkusername"/>