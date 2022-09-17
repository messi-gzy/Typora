# Node.JS

### 一、目录

### 二、初识

##### 1、运行**js**文件

在文件路径中运行命令行

```apl
node hello.js
```

![](https://pic.imgdb.cn/item/629832aa0947543129c3d269.png)

| 按键         | 功能          |
| ---------- | ----------- |
| :arrow_up: | 定位到上一次执行的命令 |
| tab        | 快速补全路径      |
| esc        | 清空当前命令      |
| cls        | 清空终端        |

### 三、fs文件系统模块

#### 1、初始化

导入

```javascript
const fs=require('fs')
```

#### 2、读取文件内容

###### 1、读取文件

<img src="https://pic.imgdb.cn/item/629835f80947543129c78dfc.png" style="zoom:50%;" />

```javascript
fs.readFile('./hello.js','utf8',function(err,data){
    console.log(err)
    console.log(data)
})
```

###### 2、判断文件读取成功

```javascript
fs.readFile('./hello.js','utf8',function(err,data){
    if(err){
        return console.log(err.message)
    }
    console.log(+data)
})
```

#### 3、写入文件

<img src="https://pic.imgdb.cn/item/62983f8f0947543129d33b51.png" style="zoom:50%;" />

```javascript
fs.writeFile('./test.txt','maxin','utf8',function(err){
    if(err){
        console.log(err)
    }
    console.log("success");
})
```

#### 4、路径动态拼接

> **相对路径为执行目录动态拼接出来的路径**

```
__dirname //表示当前文件所处的目录
```

### 四、path路径模块

##### 1、初始化

```javascript
const path=require('path')
```

##### 2、路径拼接

> **path.join()**

```javascript
const path=require('path')

let pathTest=path.join(__dirname,'/test.txt')
console.log(pathTest);
```

##### 3、获取路径中文件名

> **path.basename()**

```javascript
const path=require('path')

let pathTest=path.join(__dirname,'/test.txt')
console.log(pathTest);//E:\Data\Node.js\study\path\test.txt
console.log(path.basename(pathTest,'.txt'));//test
```

##### 4、获取路径中的文件拓展名

> **path.extname()**

```javascript
const path=require('path')

let pathTest=path.join(__dirname,'/test.txt')
console.log(path.extname(pathTest));//.txt
```

### 五、http 模块

##### 1、初始化

```javascript
const http=require('http')
```

##### 2、创建服务器

<img src="https://pic.imgdb.cn/item/62986f1f0947543129116514.jpg" style="zoom:50%;" />

```javascript
const http=require('http')
//创建服务器示例
const server=http.createServer()
//监听客户端
server.on('request',function(req,res){
    console.log("start");
})

//启动服务器

server.listen(8090,function(){
    console.log("running");
})
```

##### 3、请求数据

```javascript
const http=require('http')
//创建服务器示例
const server=http.createServer()
//监听客户端
server.on('request',(req)=>{
    const url=req.url;
    const method=req.method
    console.log("start");
    console.log(url+"  "+method);
})

//启动服务器

server.listen(8090,function(){
    console.log("running");
})
```

##### 4、响应对象

```javascript
const http=require('http')
//创建服务器示例
const server=http.createServer()
//监听客户端
server.on('request',(req,res)=>{
    console.log("start");
    res.setHeader('Content-Type','text/html; charset=utf-8')//响应头，解决乱码
    res.end("你好")//向客户端响应内容
})

//启动服务器

server.listen(8090,function(){
    console.log("running");
})
```

```javascript
const fs = require('fs');
const http=require('http');
const path = require('path');
//创建服务器示例
const server=http.createServer()
//监听客户端
server.on('request',(req,res)=>{
    console.log("start");
    res.setHeader('Content-Type','text/html; charset=utf-8')//响应头，解决乱码
    //res.end("<h1>你好</h1>")//向客户端响应内容
    const requestPath=path.join(__dirname,'../','index.html')
    fs.readFile(requestPath,'utf-8',function(err,data){
        if(err){
            return console.log(err);
        }
        res.end(data)
    })
})

//启动服务器

server.listen(8090,function(){
    console.log("running");
})
```

### 六、模块化

##### 1、概念

大文件拆分为多个模块，可以调用

##### 2、加载模块

```javascript
//加载内置模块
const fs=require('fs')

//加载自定义模块
const custom=require('./custom')

//加载第三方模块
const electron=require('electron')
```

##### 3、模块作用域

> 变量和方法等只能在当前模块使用

##### 4、导出接口

----------**module 对象**

> module.exports 将成员共享出去
> 
> 默认为一个空对象

- ```javascript
  module.exports=test //只能导出一个方法
  ```

- ```javascript
  module.exports.test=test
  ```

- ```javascript
  module.exports = {
      test1,
      test2
  }  //以对象方法导出
  
  test.test1()
  test.test2()
  ```

- ```javascript
  export.test1=test1
  export.test2=test2
  
  test.test1()
  test.test2()
  ```

==永远以**module.exports**导出的接口为主==

> module.exports===exports

##### 5、模块化规范

CommonJS

### 七、包管理

##### 1、包概念

> 第三方封装的包

##### 2、体验

- 安装

```shell
npm install moment
npm i moment
```

- 官网

> https://www.npmjs.com/

- 安装指定版本的包

```shell
npm install moment@2.22.2
```

> 不用删除之前的包

- 包管理
  
  <img src="https://pic.imgdb.cn/item/6299ac3109475431297b6194.png" style="zoom: 67%;" />

- 一次性安装所有包

```shell
npm install
```

- 卸载包

```shell
npm uninstall moment
```

##### 3、包管理配置文件

------------**package.json**

<img src="https://pic.imgdb.cn/item/6299ade109475431297d905b.png" style="zoom:50%;" />

- dependencies

> 上线也需要

- devDependencies

> 上线不需要，测试需要

```shell
npm install --save-dev webpack
```

##### 4、镜像

###### 1、查看当前镜像源

```shell
npm config get registry
```

![](https://pic.imgdb.cn/item/6299b2c40947543129843bff.png)

###### 2、切换淘宝镜像源

```shell
 npm config set registry=https://registry.npm.taobao.org/
```

###### 3、nrm工具

> 更方便的安装

```shell
npm install nrm -g
```

- 查看所有镜像源

```shell
nrm ls
```

<img src="https://pic.imgdb.cn/item/6299b6a709475431298931a6.png" style="zoom:50%;" />

- 切换镜像源

```shell
nrm use taobao
```

##### 5、包分类

###### 1、项目包

- 开发依赖包
  
  > devDependencies
  > 
  > ```shell
  > npm install ... -D
  > ```

- 核心依赖包
  
  > dependencies
  > 
  > ```shell
  > npm install ...
  > ```

###### 2、全局包

- 目录

> C:\Users\MateBook13\AppData\Roaming\npm\node_modules
> 
> 工具性质的包

- 安装全局包

```shell
npm install ... -g
```

- 卸载全局包

```shell
npm uninstall ... -g
```

##### 6、开发自已的包

###### 1、初始化

```shell
npm init -y
```

```json
{
  "name": "outs_tools",
  "version": "1.0.0",
  "description": "测试",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

###### 2、开发

```javascript
const date=require('./src/dateFormat')
const html=require('./src/htmlEscape')

module.exports={
    ...date,
    ...html
}
```

<img src="https://pic.imgdb.cn/item/6299d2ec0947543129aff14f.png" style="zoom:50%;" />

<img src="https://pic.imgdb.cn/item/6299d2ec0947543129aff13c.png" style="zoom:50%;" />

###### 3、发布包

1、登录

```shell
npm login
```

2、发布

> 包名不能相同

> 切换到根目录

```shell
npm publish
```

<img src="https://pic.imgdb.cn/item/6299d7ea0947543129b6629e.png" style="zoom: 67%;" />

3、删除已经发布的包

```shell
npm unpublish ... --force
```

![](https://pic.imgdb.cn/item/6299da090947543129b8c0fd.png)

### 八、Express

-----------**web**开发框架

##### 1、基本服务器

###### 1、创建基本服务器

```javascript
const express=require('express')
//创建Web服务器
const app=express()

app.listen(8090,()=>{
    console.log("running");
})
```

###### 2、监听*Get*和*Post*的请求

```javascript
app.get('/usr',(req,res)=>{
    res.send({
        name:"maxin",
        age:21,
        grilfriend:"gzy"
    })
})

app.post('/usr',(req,res)=>{
    res.send("POST响应成功")
})
```

###### 3、获取*URL*携带的查询参数

```javascript
http://127.0.0.1:8090/?name=maxin

app.post('/',(req,res)=>{
    console.log(req.query)
    res.send("POST响应成功")
})
```

###### 4、获取*URL*的动态参数

```javascript
http://127.0.0.1:8090/usr/3/hello

app.get('/usr/:id/:name',(req,res)=>{
    console.log(req.params)
    res.send(req.params)
})
```

##### 2、静态资源托管

###### 1、单个资源托管

```javascript
http://127.0.0.1:8090/3-1.png

const express=require('express')
//创建Web服务器
const app=express()

//对外提供资源
app.use(express.static('../resources'))//文件夹


app.listen(8090,()=>{
    console.log("running");
})
```

###### 2、托管多个资源目录

```javascript
const express=require('express')
//创建Web服务器
const app=express()

//对外提供资源
app.use(express.static('../resources'))//文件夹
app.use(express.static('../public'))//文件夹

app.listen(8090,()=>{
    console.log("running");
})
```

###### 3、挂载路径前缀

```javascript
http://127.0.0.1:8090/resources/3-1.png

const express=require('express')
//创建Web服务器
const app=express()

//对外提供资源
app.use('/resources',express.static('../resources'))//文件夹

app.listen(8090,()=>{
    console.log("running");
})
```

##### 3、路由

> 映射关系

###### 1、概念

> - 请求类型
> - 请求URL
> - 处理函数
> 
> 先后顺序匹配

###### 2、使用

1. 简单使用
   
   ```javascript
   const express=require('express')
   
   const app=express()
   
   app.get("/",(req,res)=>{
       res.send('hello')
   })
   
   app.post("/",(req,res)=>{
       res.send('world')
   })
   
   app.listen(8090,()=>{
       console.log("start");
   })
   ```

2. 模块化路由
   
   <img src="https://pic.imgdb.cn/item/629f3b540947543129db3fce.png" style="zoom: 50%;" />
   
   ```javascript
   const express=require('express')
   
   const userRouter=require('./express-module')
   
   //注册路由模块
   const app=express()
   app.use(userRouter)
   
   app.listen(8090,()=>{
   
   })
   ```

3. 添加前缀
   
   ```javascript
   app.use("/api",userRouter)
   ```

##### 4、中间件

###### 1、概念

> 业务流程中的中间处理环节

###### 2、流程处理

<img src="https://pic.imgdb.cn/item/629f3efd0947543129dff635.jpg" style="zoom:50%;" />

###### 3、格式

<img src="https://pic.imgdb.cn/item/629f41c00947543129e39b1a.jpg" style="zoom:150%;" />

###### 4、next（）

> 把流转关系转交给下一个中间件或路由，多个中间件连续调用的关键

```javascript
const middleFunction=function(req,res,next){
    console.log("中间件函数")
    next()
}
```

###### 5、全局中间件

```javascript
const middleFunction=function(req,res,next){
    console.log("中间件函数")
    next()
}
app.use(middleFunction)//注册全局生效函数
```

```javascript
app.use((req,res,next)=>{
    console.log("简化中间件")
    res.send("gzysb")
})
```

多个全局中间件

按进入顺序排序

```javascript
app.use((req,res,next)=>{
    console.log("中间件1")
    next()
})

app.use((req,res,next)=>{
    console.log("中间件2")
    next()
})
```

###### 6、局部中间件

```javascript
const mv=(req,res,next)=>{
    console.log("局部中间件")
    next()
}

app.get('/',mv,(req,res)=>{
    res.send("home")
})
```

多个局部中间件

<img src="https://pic.imgdb.cn/item/62a0284f0947543129c9f772.png" style="zoom:50%;" />

###### 7、注意事项

1. 一定在路由前注册中间件
2. keyi多个连续中间件
3. next（）
4. 逻辑清晰
5. ***中间件共享（req,res）***

##### 5、中间件的分类

###### 1、应用级别的中间件

> app.use()  | app.get()  | app.post()

###### 2、路由级别的中间件

> express.Router()

###### 3、错误级别的中间件

```javascript
app.get('/',(req,res)=>{
   throw new Error("error")
   res.send("home")
})
//捕获异常
app.use((err,req,res,next)=>{
    console.log("error"+err.message)
    res.send(err.message)
   // next()
})
```

> ==***错误中间件注册到所有路由之后***==

###### 4、内置中间件

1. express.static  //静态资源

2. express.json  //解析JSON  （4.16.0+）
   
   ```javascript
   app.use(express.json())
   ```

3. express.urlencodes  //解析URL-encoded 数据 （4.16.0+）
   
   ```javascript
   app.use(express.urlencoded({ extended :false}))
   
   app.post('/',(req,res)=>{
       console.log(req.body)
       res.send("home")
   })
   ```

###### 5、第三方中间件

body-parser

```java
const express=require('express')
const parser =require('body-parser')
const app =express()

app.use(parser.urlencoded({ extended :false}))

app.post('/',(req,res)=>{
    console.log(req.body)
    res.send("home")
})
```

###### 6、req.body

***必须配置解析表单的中间件才能拿到数据***

<img src="https://pic.imgdb.cn/item/62a0327e0947543129d60f40.png" style="zoom: 50%;" />

##### 

###### 7、自定义中间件

1. 监听data,end数据
   
   ```javascript
   app.use((req,res,next)=>{
       let str=''
   
       req.on('data',(chunk)=>{
           str+=chunk
       })
       req.on('end',()=>{
           console.log(str)
       })
   })
   ```

2. querystring模块
   
   <img src="https://pic.imgdb.cn/item/62a70a890947543129c3ab12.png" style="zoom:67%;" />

###### 8、接口

```javascript
router.get('/get',(req,res)=>{
    const query=req.query

    res.send({
        status:0,
        msg:"GET成功",
        data:query
    })
})

router.post('/post',(req,res)=>{
    const body=req.body

    res.send({
        status:0,
        msg:"POST成功",
        data:body
    })
})
```

###### 9、解决跨域

> **CORS** 配置
> 
> <img src="https://pic.imgdb.cn/item/62a7148a0947543129d65654.png" style="zoom:50%;" />

响应头：

1. > Access-Control-Allow-Origin : <origin> | *     请求地址

2. > Access-Control-Allow-Headers : <origin> | *     请求地址

3. > Access-Control-Allow-Methods: <origin> | *     请求方式

4. a
