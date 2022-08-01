# Rust命令语句

## 一、目录

## 二、命令行

### 1、编译

##### 1、rustc

```shell
rustc main.rs
```

`rustc 只适合简单项目`

##### 2、Cargo

###### 1、创建项目

```shell
cargo new hello_world
```

###### 2、Cargo.toml

> 配置文件

![](https://pic.imgdb.cn/item/62e37542f54cd3f9375a8d97.png)



###### 3、构建和运行

1. 构建
   
   ```powershell
   cargo build
   ```

2. 运行
   
   ```
   .\target\debug\main.exe
   ```



`直接运行`

```
cargo run
```



###### 4、检查

> 检查代码，不产生可执行文件

```
cargo check
```



###### 5、发布构建

```
cargo build --release
```
