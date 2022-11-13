# TypeScript

​	<mark>TypeScript</mark> 是由微软开发的一款开源的编程语言，TypeScript 是 Javascript 的超集，遵循最新的 ES6、ES5 规范，TypeScript 扩展了 JavaScript 的语法。最新的 Vue 、React 也可以集成 TypeScript。Nodejs 框架中的 Nestjs、midway 中用的就是 TypeScript 语法。

​	此笔记适合有JavaScript语法基础的人阅读

- $\textcolor{#e18a3b}{【一】}$[介绍和安装](#1)
- $\textcolor{#e18a3b}{【二】}$[基础](#2)
- $\textcolor{#e18a3b}{【三】}$[介绍](#3)

## 一、介绍和安装

<a id="1"><!---介绍和安装---></a>

### 1.1、介绍

![](https://pic1.imgdb.cn/item/636a639216f2c2beb183f03e.png)

​	<mark>TypeScript</mark>是`JavaScript`的超集，TypeScript 不能被浏览器直接执行，但是 TypeScript 可以先编译成 JavaScript，再在浏览器或 nodejs 上运行。

​	<mark>ArkTS</mark>是华为自研的开发语言。它在`TypeScript`的基础上，匹配`ArkUI`框架，**扩展了声明式UI、状态管理等**相应的能力，让开发者以更简洁、更自然的方式**开发跨端应用**。

### 1.2、安装

#### 1、安装node

不再概述

#### 2、安装typescript

> 全局安装

```bash
npm install -g typescript
```

`检查`

```
tsc --version
```

### 1.3、编译

#### 1、编译

```
tsc test.ts
```

编译生成js文件，再浏览器或者node中运行。

#### 2、配置文件

## 二、基础

- $\textcolor{#2a6e3f}{【01】}$ [数据类型](#2.1)
- $\textcolor{#2a6e3f}{【02】}$ [](#2.2)
- $\textcolor{#2a6e3f}{【03】}$ [](#2.3)
- $\textcolor{#2a6e3f}{【04】}$ [](#2.4)
- $\textcolor{#2a6e3f}{【05】}$ [](#2.5)
- $\textcolor{#2a6e3f}{【06】}$ [](#2.6)
- $\textcolor{#2a6e3f}{【07】}$ [](#2.7)
- $\textcolor{#2a6e3f}{【08】}$ [](#2.8)

### 2.1、数据类型<a id="2.1">💛</a>

#### 1、类型声明赋值

```typescript
// 声明一个变量，指定类型为number，不可更改
let a: number = 10;
let array: string[] = ["a", "b", "c"];
```

==格式==

```typescript
let <name>: type = <value>
```

> 如果变量**只赋值，未声明**，编译器会自动对变量进行类型检测并规定。
>
> ```
> let test=10;
> ```

#### 2、基本数据

