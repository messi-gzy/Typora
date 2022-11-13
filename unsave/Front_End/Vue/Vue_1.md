# Vue

​	Vue 是一款用于构建用户界面的 JavaScript 框架。它基于标准 HTML、CSS 和 JavaScript 构建，并提供了一套声明式的、组件化的编程模型，帮助你高效地开发用户界面。无论是简单还是复杂的界面，Vue 都可以胜任。

## 一、基础

#### 1、实例

```javascript
const vm =new Vue({
            el:'#root'
        })
```

#### 2、容器

```javascript
<div id="root">
      <h1>hello{{name}}</h1>
</div>
```

> ==实例与容器一一对应==

#### 3、插值语法

```javascript
<div id="root">
    <h1>hello{{name}}</h1>
</div>
<script>
    Vue.config.productionTip=false
    new Vue({
        el:'#root',
        data: {
            name:"maxin"
        },
    })
</script>
```

> 标签体

![](https://pic.imgdb.cn/item/62ed25c68c61dc3b8eaaef56.png)

> 插入值为**JS表达式**



> `引号中`指令语法

```javascript
<a v-bind:href="url">{{url}}</a>
<a href="url">{{url}}</a>
```

#### 4、数据绑定

###### 	1、v-bind （单向绑定）

###### 	2、v-model （双向绑定）

> ​		双向绑定一般用在 **<u>表单元素</u>**上

`data函数式`

```javascript
data:function() {
    return{
        name:"maxin",
        url:"https://github.com"
    }
}
```



#### 5、**MVVM 模型** 

1. M：模型(Model) ：对应 data 中的数据 

2. V：视图(View) ：模板 

3. VM：视图模型(ViewModel) ： Vue 实例对象

![](https://pic.imgdb.cn/item/62ee26d28c61dc3b8e9295d1.png)

```javascript
let person = {
    name:"ma"
}
Object.defineProperty(person,'age',{
    value:20,//值
    enumerable:true, // 可枚举（可输出）
    writable:true  //可修改
    configurable:true //可删除
})
```



#### 6、数据代理

##### 1、set

```javascript
vm.name = "sdad"
```

##### 2、get

```
vm.name
```



#### 7、事件处理

##### 1、点击事件

```javascript
<button v-on:click = "showMessage">{{message}}</button> 


const vm=new Vue({
    el:'#root',
    data: {       
        name:"maxin",
        url:"https://github.com",
        message:"点我提示信息"
    },
    methods: {
        showMessage(){
            alert('hello')
        }  
    },
})   
```

> 1. v-on:click = "showMessage"
> 2. @click = "showMessage"
>
> **<button *v-on:click* = "showMessage($event,20)">{{message}}</button>**`方法传参`

1、使用 v-on:xxx 或 @xxx 绑定事件 ,其中xxx是事件名。

2、时间的回调需要配置在methods对象中,最终在vm中

3、methods中配置的函数,不要用箭头函数!否则this就不是vm了。

4、methods中配置的函数,都是被Vue所管理的函数,this的指向是vm或 组件实例对象。

5、@click = "demo" 和 @click = "demo($event)"效果一致,但后者可以传参



##### 2、事件修饰符

1. .prevent : 阻止事件的默认行为 event.preventDefault() 

2. .stop : 停止事件冒泡 event.stopPropagation()
3. .once: 事件只发生一次
4. .capture:事件捕获模式
5. .self:只有event.target是当前操作的元素时才触发事件
6. passive: 事件默认行为立即执行，不等待返回值



##### 3、键盘事件

*1.Vue中常用的按键别名：*

​        *回车 => enter*

​        *删除 => delete (捕获“删除”和“退格”键)*

​        *退出 => esc*

​        *空格 => space*

​        *换行 => tab (特殊，必须配合keydown去使用)*

​        *上 => up*

​        *下 => down*

​        *左 => left*

​        *右 => righ*

  *2.Vue未提供别名的按键，可以使用按键原始的key值去绑定，但注意要转为kebab-case（短横线命名*

  *3.系统修饰键（用法特殊）：ctrl、alt、shift、meta*

​        *(1).配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发。*

​        *(2).配合keydown使用：正常触发事件*

  *4.也可以使用keyCode去指定具体的按键（不推荐*

  5.Vue.config.keyCodes.自定义键名 = 键码，可以去定制按键别名



#### 8、计算属性与监视

##### 8.1、计算属性

> computed



##### 8.2、监视

> watch



