# Node.JS

### 一、目录

### 二、初识

##### 1、运行**js**文件

在文件路径中运行命令行

```apl
node hello.js
```

![](https://pic.imgdb.cn/item/629832aa0947543129c3d269.png)

| 按键       | 功能                   |
| ---------- | ---------------------- |
| :arrow_up: | 定位到上一次执行的命令 |
| tab        | 快速补全路径           |
| esc        | 清空当前命令           |
| cls        | 清空终端               |

### 三、fs文件系统模块

#### 1、初始化

导入

```javascript
const fs=require('fs')
```

#### 2、读取文件内容

###### 	1、读取文件

<img src="https://pic.imgdb.cn/item/629835f80947543129c78dfc.png" style="zoom:50%;" />

```javascript
fs.readFile('./hello.js','utf8',function(err,data){
    console.log(err)
    console.log(data)
})
```

###### 	2、判断文件读取成功

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

**module 对象**

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

