# Vue

<a id="0"><!----目录---></a>

$\textcolor{#e18a3b}{【一】}$**[生命周期](#1)**

$\textcolor{#e18a3b}{【二】}$**[组件](#2)**

$\textcolor{#e18a3b}{【三】}$**[Vue脚手架](#3)**

$\textcolor{#e18a3b}{【一】}$**[生命周期](#1)**

$\textcolor{#e18a3b}{【一】}$**[生命周期](#1)**

## 一、生命周期

<a id="1"><!----生命周期---></a>

### 1、定义

​	每一个`vue`实例从创建到销毁的过程，就是这个`vue`实例的生命周期。在这个过程中，他经历了**从开始创建、初始化数据、编译模板、挂载Dom、渲染→更新→渲染、卸载等一系列过程**。每个 `Vue` 组件实例在创建时都需要经历一系列的初始化步骤，比如**设置好数据侦听，编译模板，挂载实例到 DOM，以及在数据改变时更新 DOM**。在此过程中，它也会运行被称为生命周期钩子的函数，让开发者有机会在特定阶段运行自己的代码。

### 2、生命周期

![](https://pic1.imgdb.cn/item/6370bae516f2c2beb1e20ea5.png)

Vue在关键时刻使用‘钩子’将自已设定的函数取出来执行，形成生命周期

#### 2.1、挂载流程

##### 1、beforeCreate

> 初始化后（**数据代理未开始**）

<!---注意--->

- **无法**通过对象访问**data**数据和**methods**方法

##### 2、created

> 初始化后（**数据监测，数据代理**）

- 可以通过对象访问**data**数据和**methods**方法

##### 3、beforeMount

> 在Vue解析模版生成虚拟 `DOM`后

- 页面呈现未经Vue编译的DOM结构

- 所有对DOM的操作最终不起作用（因为在这之后Vue开始编译，生成DOM）

##### 4、mounted

> 在经过Vue编译后，将真实DOM插入页面

`Vue`完成模版的解析并把<mark>**初始**</mark>的**真实DOM元素放入页面后**（挂载完毕）调用**mounted**

建议在此执行：

- 开启定时器
- 发送网络请求
- 订阅消息
- 绑定自定义事件
- 初始化操作等

#### 2.2、更新流程

##### 1、beforeUpdate

> 在挂载流程结束后执行，且数据发生变化时调用

- **数据更新，但是页面还未刷新**
- 页面和数据未同步

##### 2、updated

> 根据新数据**生成新的虚拟DOM，然后与旧的虚拟DOM比较**，然后实现页面更新

- **数据和页面同步**

#### 2.3、销毁流程

##### 1、beforeDestroy

> 调用 `xxx.$destroy()`函数后
>
> - 完全销毁一个实例
> - 清理与其他的实例的链接，解绑它的全部指令及自定义事件监听器
> - 可以读取数据，但是**不在触发更新流程**

建议在此执行：

- 关闭定时器
- 取消订阅消息
- 解绑自定义事件等收尾操作

##### 2、destroy

> 在清理与其他的实例的链接，解绑它的全部指令及自定义事件监听器后执行

## 二、组件

<a id="2"><!----组件---></a>

​	组件允许我们将 UI 划分为独立的、可重用的部分，并且可以对每个部分进行单独的思考。

传统方式编写存在的问题：

1. 依赖关系比较混乱，不好维护
2. 代码复用率不高

`组件`

实现应用中局部功能代码和资源的集合

![](https://pic1.imgdb.cn/item/637111de16f2c2beb16f2aff.png)

#### 1、非单文件组件

##### 1.1、创建子组件

> <mark>注意</mark>
>
> - 创建组件时不需要指定 **el**
> - **data必须写成函数式**

###### 1、school

```javascript
const school = Vue.extend({
    template: `
    <div>
        <h2>学校名称：{{school.name}}</h2>
        <h2>学校地址：{{school.address}}</h2>
    </div>
    `,
    data() {
        return {
            school: {
                name: "华北电力大学",
                address: "北京昌平"
            }
        }
    },
})
```

###### 2、student

```javascript
const student = Vue.extend({
    template: `
    <div>
        <h2>学生姓名：{{student.name}}</h2>
        <h2>学生年龄：{{student.age}}</h2>
    </div>
    `,
    data() {
        return {
            student: {
                name: "MaXin",
                age: 20
            }
        }
    }
})
```

##### 1.2、注册组件

> - 需要写**el**
> - 需要写**components**

```javascript
const vm = new Vue({
    el: "#root",
    // 注册组件
    components: {
        school: school,
        student: student
    }
})
```

```html
<div id="root">
    <school></school>
    <hr>
    <student></student>
</div>
```

<mark>**全局注册**</mark>

```javascript
Vue.component('student',student)
Vue.component('school',school)
```

##### 1.3、注意



##### 1.4、组件的嵌套

```javascript
school = Vue.extend({
    template: `
    <div>
        <h2>学校名称：{{school.name}}</h2>
        <h2>学校地址：{{school.address}}</h2>
        <button @click="showName">点我提示</button>
        <student></student>
    </div>
    `,
    data() {
        return {
            school: {
                name: "华北电力大学",
                address: "北京昌平"
            }
        }
    },
    methods: {
        showName(){
            alert(this.school.name)
        }
    },
    components:{
        student
    }
})
```

##### 1.5、VueComponent

> 组件的实例对象，由vm实例对象掌控

#### 2、单文件组件

```vue
<template>
  <div class="demo">
    <h2>学校名称：{{ student.name }}</h2>
    <h2>学校地址：{{ student.age }}</h2>
    <button @click="showName">点我提示</button>
  </div>
</template>
  
<script>
export default Vue.extend({
  name: "Student",
  data() {
    return {
      student: {
        name: "gzy",
        age: 18,
      },
    };
  },
  methods: {
    showName(){
        alert(this.student)
    }
  },
});
</script>
  
<style>

</style>
```

---

[返回顶部](#0)

## 三、Vue脚手架

<a id="3"><!----Vue脚手架---></a>

#### 1、安装脚手架

##### 1.1、安装node

直接官网下载安装

##### 1.2、修改淘宝镜像

```
npm config set registry https://registry.npm.taobao.org
```

##### 1.3、安装脚手架

```bash
npm install -g @vue/cli
```

##### 1.4、验证

```
vue -V
```

#### 2、新建项目

1. 切换到自已选择的目录下

2. 打开命令行

3. ```
   Vue create <XXXX>
   ```

   <!--XXXX是自已起的名字--->

   > 根据自已的需求选择相应版本
   >
   > 不太熟练可以选中default Vue2

4. ```
   cd <XXXX>
   # 进入自已创建的文件
   ```

5. ```
   npm run serve
   ```

   打包运行

6. 按照输出的文件路径在浏览器中访问

   > http://localhost:8080/

#### 3、分析脚手架

![](https://pic.imgdb.cn/item/6372427c16f2c2beb1eabb54.png)

启动后执行main.js加载App组件，然后相继加载子组件，插入到html中显示页面

##### 3.1、render

```vue
render:createElement=>{
	return createElement('h1','hello')
}

/********/
render:e=>return e('h1','hello')
```

#### 4、修改默认配置

```
 vue inspect > output.js
```

查看配置文件输出到 output.js文件中



[返回顶部](#0)
