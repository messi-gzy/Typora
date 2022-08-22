# CSS

##  一、 目录<a name="目录"></a>



## 二、 选择器

> ```html
> p {
> 
> }
> ```



#### 		2.2 ， 类选择器

- 单类选择器

  > ```css
  > .类名 {
  >        ........
  > }
  > <li class="类名"></li
  > ```

- 多类选择器

#### 		2.3，  id选择器 	

> ```css
> /*只能被调用一次*/
> #id名 {
>      .............
> }
> <div id="id名">
> ```
>

#### 		2.4，  通配符选择器

> ```css
> * {
> //(所有标签都改变)
> }
> ```
>

#### 	2.5,     复合选择器

##### 			2.5.1，  后代选择器

> ```css
> .son li a {
> 		........
> }
> ```

##### 			2.5.2，  子选择器

> ```css
> .father > a {
> 		........
> }
> ```

##### 			2.5.3，  并集选择器

> ```css
> div,p {
> 		.......
> }
> ```

##### 			2.5.4，  伪类选择器

- 链接伪类选择器

  > ```css
  > a:link {.....}	/*选择未被访问*/
  > a:visited{.....}  /*已被访问*/
  > a:hover{.....}  /*鼠标指针位于上方*/
  > a:active{.....}  /*活动链接（鼠标按下未弹起）*/
  > ```

- 表单伪类选择器

  > ```css
  > /*focus~~~~*/
  > input :focus {
  > 		......
  > }
  > ```

  
  
  跳转到[目录](#目录)
  
  

## 三、 CSS字体属性

| font-family  | 字体 （多字体逗号隔开，加引号）                              |
| ------------ | ------------------------------------------------------------ |
| font-Size    | 字体大小（PX：像素）                                         |
| font-weight  | 字体粗细（数字）{默认400（normal），最大700（bold}           |
| font-style   | 字体风格{italic ：倾斜    normal: 普通}                      |
| font复合写法 | {-style -weight -size/line-height -family}(==顺序不可颠倒==) |



跳转到[目录](#目录)



## 四、  文本属性

#### 	4.1，  文本颜色

​			 **color**    

#### 	4.2，  水平对齐

​			**text-align**  

#### 	4.3，  装饰文本

​			**text-decoration**  

- underline : 下划线

- overline : 上划线
- line-through : 删除线
- ==none : 取消（$\textcolor{red}{无装饰线})$==

#### 	4.4，  文本缩进

​		text-indent

#### 	4.5，  行间距

​		line-height



跳转到[目录](#目录)



## 五、 引入方式

#### 	5.1，   内部样式表

####     5.2，   行内样式表

#### 	5.3，   外部样式表

> 使用<link>标签在<head>引入文件
>
> ```html
> <link rel="stylesheet" href="xxx.css">
> ```



跳转到[目录](#目录)



## 六、 Emmet语法

#### 	6.1，  快速生成HTML语法

<img src="E:\图片\Saved Pictures\Screenshot_20211015_234208.jpg" alt="Screenshot_20211015_234208"  />

#### 	6.3，  快速格式化代码

​				$\textcolor{red}{Shift+Alt+F}$



​	跳转到[目录](#目录)



## 七、  CSS的元素显示模式

#### 	7.1,     元素

##### 			7.1.1，  块元素

```html
<div>......<p><ul><li>
```

> 1.  ：独占一行
> 2.  ：可控制
> 3.  ：默认父元素
> 4.  ：里面可以放行内/块元素
> 5.  ：文字标签无法放块元素

##### 			7.1.2，  行内元素

```html
<sapn>.....<a><strong>
```

> 1.  ：一行可显示多个
> 2.  ：不可控制高度
> 3.  ：默认本身容量宽度
> 4.  ：行内只能放行内元素
>    - 链接不能放链接
>    - <a>中不能放块元素

##### 			7.1.3，  行内块元素

```html
<img>....<input><td>
```

> 1.  ：设置大小
> 2.  ：一行放多个

#### 	7.2，  元素显示模式的转换

##### 			7.2.1，  行内--->块

​			==display : block==

##### 			7.2.2，  块--->行内

​			==display : inline==

##### 			7.2.3，  ----->行内块

​			==display : inline-block==



跳转到[目录](#目录)



## 八、  CSS背景

#### 	8.1,     背景颜色

​		**background-color :**

#### 	8.2,     背景图片

​		==**background-image :   url(......);**==

#### 	8.3,     背景平铺

​		==**background-repeat:**==

1. repeat
2. no-repeat
3. repeat-x
4. repeat-y

#### 	8.4,     背景图片位置

​		**background position : x y**

##### 	8.4.1，   方位名词

​		***<u>$\textcolor{red}{(前后顺序无关)}$</u>***

​		x:  left / center / right

​		y:  top / center / botton

##### 	8.4.2，   精确单位

​		background-position : x  y   ==(前后位置不可变)==

##### 	8.4.3，   混合单位

​		**==$\textcolor{Orange}{使用时顺序不可变}$==**

#### 	8.5,     图像固定

​		background-attachment

- scoll : 滚动
- fixed : 固定

#### 	8.6,     背景复合写法

​		顺序：图片、地址、平铺、滚动、位置

> ```css
> background:........
> ```

#### 	8.7,     背景色半透明

```css
background : rgba(0,0,0,0.3)/*a:透明度 0~1*/
```



跳转到[目录](#目录)



## 九、  盒子模型

#### 9.1，  盒子模型组成

#### 9.2，  边框

#### 9.3，  表格的边框

#### 9.4，  圆角边框

#### 9.5，  盒子阴影



跳转到[目录](#目录)



## 十、  浮动



> 浮动的元素不会压住底下的图片和文字
>

## 十一、  定位

| top    | 顶部   |
| ------ | ------ |
| bottom | 底部   |
| left   | 左偏移 |
| right  | 右便宜 |

#### 11.1，  相对定位

position : relative

> - 拖标后继续占有原有位置（不拖标）

> - 相对自身原来的位置移sa
> - 限制绝对定位

#### 11.2，  绝对定位

position : absolute

1. **以父级为定位约束**（如果没有父级或者父级没有定位，则已浏览器为父元素）
1. 以最近一级带有定位的父元素为父级定位
2. **脱标后不在占有原有位置**

> ### 子绝父相
>
> - 子级绝对定位
>
> - 父级相对定位

#### 11.3，  固定定位

position : fixed

1. **父级为浏览器可视窗口**，和父元素无关系。
2. 脱标后不在占有原有位置
2. 宽度计算 ：calc(100% - 100px)

#### 11.4，  粘性定位

position : sticky

(部分位置固定，部分移动)

- 拖标后继续占有原有位置
- 以浏览器的可视窗口为参照点
- 必须添加至少一个偏移值

#### 11.5，  定位叠放次序

**==z-index : (int?)==**

> 只有定位的盒子才有此属性

#### 11.6、属性

> 添加定位后可以直接设置宽高

#### 11.7、元素的显示与隐藏

###### 1、display

- display : none ; 隐藏对象
- display : block;  显示对象

==**隐藏后位置也不再占有**==

###### 2、visibility

- visibility : hidden；元素隐藏
- visibility : visible;元素可视

**==隐藏后位置继续占有==**

###### 3、overflow 溢出

- overflow :

| visible | 显示所有内容，不隐藏 |
| ------- | -------------------- |
| auto    | 显示滚动条           |
| scroll  | 自动滚动条           |
| hidden  | 隐藏多出来的部分     |



## 十二、高级技巧

#### 1、精灵图(sprites)

> 减少服务器的接受和返回的次数

###### 1、主要背景图片，定位背景图片位置，一张图片多次使用调

按照坐标轴调整

#### 2、字体图标

#### 3、三角

```css
width :0;
height:0;
border :10px solid transparent;
border-top-color : pink;
```

#### 4、用户界面样式

1. 更改鼠标样式

   ```css
    {cursor : pointer }
   ```

   | 属性值      | 描述      |
   | ----------- | --------- |
   | default     | 小白 默认 |
   | pointer     | 小手      |
   | move        | 移动      |
   | text        | 文本      |
   | not-allowed | 禁止      |

2. 表单轮廓线

   ```css
   {outline : none / 0;}
   ```

3. 文本域取消拖拽

   ```css
   {resize : none }
   ```

4. vertical-align

   块级元素不存在基线准则

   | baseline | 默认 ，基线 |
   | -------- | ----------- |
   | middle   | 顶端        |
   | bottom   | 中部        |
   | top      | 底端        |

5. 图片底侧空白间隙

   - vertical-align
   - display : block;

6. 溢出文字省略号显示

   文字换行

   - ```css
     white-space : normal //自动换行
     ```

   - ```css
     white-space : nowrap //取消自动换行
     ```

   溢出的隐藏

   - ```css
     overflow : hidden
     ```

   省略号

   - ```css
     text-overflow : ellipsis
     ```

   多行省略号

   - ```css
      overflow: hidden;
      text-overflow: ellipsis;
      display: -webkit-box;
      -webkit-line-clamp: 2;
      -webkit-box-orient: vertical;
     ```

7. 文字围绕浮动元素

   浮动

8. 三角强化

   ```
   .box {
           width: 0px;
           height: 0px;
           border-top: 100px solid  transparent;
           border-bottom: 0px solid rgb(32, 166, 32);
           border-left: 0px solid rgb(24, 67, 141);
           border-right: 50px solid rgb(149, 14, 117);
       }
   ```

   ![](https://pic.imgdb.cn/item/629621890947543129b640c7.png)

9. CSS初始化

## 十三、新增语法

<img src="https://pic.imgdb.cn/item/629738a40947543129c8d361.jpg" style="zoom: 33%;" />

#### 1、视频标签

```html
 <video src="...." controls="controls"></video>
```

<img src="https://pic.imgdb.cn/item/62973a030947543129caebde.jpg" style="zoom:50%;" />

#### 2、音频标签

```html
 <audio src="E:\CloudMusic\天行九歌-(动画《天行九歌》主题曲)的MP3下载_霍尊-天行九歌.mp3" controls="controls"></audio>
```

![](https://pic.imgdb.cn/item/629742ac0947543129d7d633.png)

#### 3、表单元素

![](https://pic.imgdb.cn/item/62975a520947543129f3e2b1.jpg)

![6.jpg](https://s2.loli.net/2022/06/01/4yl7eCqA9FBcOHD.jpg)

#### 4、伪类选择器

![](https://pic.imgdb.cn/item/629762960947543129fea015.jpg)

- ```css
  nth-child(even)//偶数孩子
  nth-child(odd)//奇数孩子
  nth-child(n)//公式计算 （只能为n，n从0取）
  <!--nth-child将所有孩子都排序 -->
  <!--nth-of-type将指定元素都排序 -->
  ```

#### 5、伪元素选择器

| 选择符   | 简介                     |
| -------- | ------------------------ |
| ::before | 在元素内部前面插入内容   |
| ::after  | 在元素内部的后面插入内容 |

:clap:

![](https://pic.imgdb.cn/item/62976798094754312904cb35.jpg)

####  6、盒子模型

> #### **$\textcolor{blue}{box-sizing:bordeer-box}$**

#### 7、图片模糊

```html
<style>
    img {
        filter :blur(100px);
    }
    
</style>
<body>
    <img src="../../../图片/snipaste/MacOS/macOS 11-2022-05-17-11-41-12.png" alt="">
</body>
```

> blur(...),值越大，越模糊

#### 8、过渡

![](https://pic.imgdb.cn/item/62c521345be16ec74ae51515.jpg)

```css
div {
    display: block;
    width: 100px;
    height: 100px;
    background-color: aqua;
    transition: width 1s ease 1s,height 1s ease 1s;//逗号隔开
}
```

