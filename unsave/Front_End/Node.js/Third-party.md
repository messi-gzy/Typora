# Third-party

### 一、目录

### 二、i5ting_toc

> html--->md

##### 1、安装（全局）

```shell
npm install i5ting_toc -g
```

##### 2、使用

```shell
i5ting_toc -f node.md -o
```

### 三、nodemon

##### 1、安装（全局）

```shell
npm install nodemon -g
```

##### 2、使用

```shell
nodemon app.js
```

### 四、node-gyp

### 五、log4js

### 六、MySQL

> 安装：
>
> ```bash
> npm install mysql
> ```

#### 1、配置

```javascript
const mysql = require('mysql')
// mysql 配置信息
const config = {
    host: "127.0.01",
    user: "root",
    password: "******",
    database: "test"//需要操作的数据库
};

const db = mysql.createPool(config)
```

<!--检测链接是否成功-->

```javascript
const db = mysql.createPool(config)
let sql = `SELECT 1`;
db.query(sql,(err,results)=>{
    if(err) return console.log(err.message);
    console.log(results);
})
```

<!--关闭数据库连接-->

```javascript
const db = mysql.createPool(config);


function closeMysql(connect) {
    connect.end((err) => {
        if (err) {
            console.log('关闭失败');
        } else {
            console.log('MySQL已关闭');
        }
    })
}
```

```
closeMysql(db);
```

#### 2、查询数据

```javascript
const db = mysql.createPool(config)
let sql = `SELECT * FROM emp_s;`;
db.query(sql, (err, results) => {
    if (err) return console.log(err.message);
    console.log(results.length);
    for (let index = 0; index < results.length; index++) {
        console.log(results[index]);
    }
    closeMysql(db)
})
```

#### 3、修改 数据

**==*需要执行的SQL语句中 ? 为占位符*==**

```javascript
// 需要插入的数据
let student ={
    gride:66,
    number:33
};
// 需要执行的SQL语句， 其他 ? 为占位符
let sql = `INSERT INTO student(gride,number)
            VALUES(?,?);`;
// 中间参数为需要替换 ？号的参数
db.query(sql,[student.gride,student.number], (err, results) => {
    if (err) return console.log(err.message);
// 返回值为1代表执行成功
    if(results.affectedRows === 1){
        console.log('插入成功');
    }
    closeMysql(db);
})
```

