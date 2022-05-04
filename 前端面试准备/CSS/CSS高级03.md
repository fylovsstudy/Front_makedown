## 2、移动端常见布局

![在这里插入图片描述](https://img-blog.csdnimg.cn/31944f6dcdbe424b95efb6209f9fc7d0.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

### 2.1、流式布局(百分比布局)

- 流式布局，就是百分比布局，也称非固定像素布局。
- 通过盒子的宽度设置成百分比来根据屏幕的宽度来进行伸缩，不受固定像素的限制，内容向两侧填充。

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        
        section {
            width: 100%;
            max-width: 980px;
            min-width: 320px;
            margin: 0 auto;
        }
        
        section div {
            float: left;
            width: 50%;
            height: 400px;
        }
        
        section div:nth-child(1) {
            background-color: pink;
        }
        
        section div:nth-child(2) {
            background-color: purple;
        }
    </style>
</head>

<body>
    <section>
        <div></div>
        <div></div>
    </section>
</body>
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/4898866c139346498a48354784a80789.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

### 2.2、flex布局（弹性布局）

**布局原理**

![image-20220309183236120](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220309183236120.png)

| 传统布局                       | flex弹性布局                                 |
| ------------------------------ | -------------------------------------------- |
| 兼容性好                       | **操作方便，布局极为简单，移动端应用很广泛** |
| 布局繁琐                       | **PC 端浏览器支持情况较差**                  |
| 局限性，不能再移动端很好的布局 | IE 11或更低版本，不支持或仅部分支持          |

建议：

1. 如果是PC端页面布局，我们还是传统布局。
2. 如果是移动端或者不考虑兼容性问题的PC端页面布局，我们还是使用flex弹性布局

#### 2.2.1、初体验

1. 搭建HTML结构

```html
<div>
  <span>1</span>
  <span>2</span>
  <span>3</span>
</div>
```

2. CSS样式

span 直接给宽度和高度，背景颜色，还有蓝色边框

**给 div 只需要添加 `display: flex` 即可**

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            display: flex;
            width: 80%;
            height: 300px;
            background-color: pink;
            
        }
        
        div span {
            /* width: 150px; */
            height: 100px;
            background-color: purple;
            margin-right: 5px;
            flex: 1;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
    </div>
</body>
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/3d69fd5718e84f6ea3a1fbf5846c8a48.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

#### 2.2.2、flex布局原理

flex 是 flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性，任何一个容器都可以指定为 flex 布局。

- 当我们为父盒子设为 flex 布局以后，子元素的 float、clear 和 vertical-align 属性将失效。
- 伸缩布局 = 弹性布局 = 伸缩盒布局 = 弹性盒布局 =flex布局

采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。

![在这里插入图片描述](https://img-blog.csdnimg.cn/d27de399dbd64e5db668e9d20c8b48bd.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

- 上述例子 div 就是 flex父容器。
- 上述例子 span 就是 子容器 flex项目
- 子容器可以横向排列也可以纵向排列

总结 flex 布局原理：**就是通过给父盒子添加 flex 属性，来控制子盒子的位置和排列方式。**

#### 2.2.3、flex布局常见父项属性

以下有 6 个属性是对父元素设置的

- flex-direction：设置主轴的方向
- justify-content：设置主轴上的子元素排列方式
- flex-wrap：设置子元素是否换行
- align-content：设置侧轴上的子元素的排列方式（多行）
- align-items：设置侧轴上的子元素排列方式（单行）
- flex-flow：复合属性，相当于同时设置了 flex-direction 和 flex-wrap

##### 2.2.3.1、flex-direction设置主轴方向

主轴和侧轴：在 flex 布局中，是分为主轴和侧轴两个方向，同样的叫法有：行和列、x轴和y轴

- 默认主轴方向就是 x 轴方向，水平向右
- 默认侧轴方向就是 y 轴方向，水平向下

![在这里插入图片描述](https://img-blog.csdnimg.cn/513ae11d9f4041949b450c2c1a40dc7e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

```html

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            /* 给父级添加flex属性 */
            display: flex;
            width: 800px;
            height: 300px;
            background-color: pink;
            /* 默认的主轴是 x 轴 行 row  那么y轴就是侧轴喽 */
            /* 我们的元素是跟着主轴来排列的 */
            /* flex-direction: row; */
            /* 我们可以把我们的主轴设置为 y轴 那么 x 轴就成了侧轴 */
            flex-direction: column;
        }
        
        div span {
            width: 150px;
            height: 100px;
            background-color: purple;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
    </div>
</body>
```

![image-20220309183646304](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220309183646304.png)

- flex-direction 属性决定主轴的方向（即项目的排列方向）
- 注意： 主轴和侧轴是会变化的，就看 flex-direction 设置谁为主轴，剩下的就是侧轴。而我们的子元素是跟着主轴来排列的

| 属性值         | 说明               |
| -------------- | ------------------ |
| **row**        | **默认值从左到右** |
| row-reverse    | 从右到左           |
| **column**     | **从上到下**       |
| column-reverse | 从下到上           |

##### 2.2.3.2、justify-content 设置主轴上的子元素排列方式

- justify-content 属性定义了项目在主轴上的对齐方式
- **注意： 使用这个属性之前一定要确定好主轴是哪个**

| 属性值            | 说明                                            |
| ----------------- | ----------------------------------------------- |
| **flex-start**    | **默认值从头部开始，如果主轴是x轴，则从左到右** |
| flex-end          | 从尾部开始排列                                  |
| **center**        | **在主轴居中对齐(如果主轴是 x 轴则水平居中)**   |
| **space-around**  | **平分剩余空间**                                |
| **space-between** | **先两边贴边，再平分剩余空间🔥**                 |

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            display: flex;
            width: 800px;
            height: 300px;
            background-color: pink;
            /* 默认的主轴是 x 轴 row */
            flex-direction: row;
            /* justify-content: 是设置主轴上子元素的排列方式 */
            
            /* justify-content: flex-start; */
            
            /* justify-content: flex-end; */
            
            /* 让我们子元素居中对齐 */
            /* justify-content: center; */
            
            /* 平分剩余空间 */
            /* justify-content: space-around; */
            
            /* 先两边贴边， 在分配剩余的空间 */
            justify-content: space-between;
        }
        
        div span {
            width: 150px;
            height: 100px;
            background-color: purple;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
        <span>4</span>
    </div>
</body>
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/4b70488588e54aa18ea44c39a0c0d074.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            display: flex;
            width: 800px;
            height: 400px;
            background-color: pink;
            /* 我们现在的主轴是y轴 */
            flex-direction: column;
            /* justify-content: center; */
            justify-content: space-between;
        }
        
        div span {
            width: 150px;
            height: 100px;
            background-color: purple;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
    </div>
</body>

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/eba632281ba14898b7b20f9592d34047.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

##### 2.2.3.3、flex-wrap 设置子元素是否换行

默认情况下，项目都排在一条线（又称”轴线”）上。flex-wrap属性定义，flex布局中默认是不换行的。

意思就是如果按照我们设置的盒子大小，一行只能装 3 个盒子，但是我们有 5 个盒子，那么 flex 布局默认会给我们塞上去，自动缩小盒子大小。

| 属性值   | 说明           |
| -------- | -------------- |
| nowrap   | 默认值，不换行 |
| **wrap** | **换行**       |

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            display: flex;
            width: 600px;
            height: 400px;
            background-color: pink;
            /* flex布局中，默认的子元素是不换行的， 如果装不开，会缩小子元素的宽度，放到父元素里面  */
            /* flex-wrap: nowrap; */
            flex-wrap: wrap;
        }
        
        div span {
            width: 150px;
            height: 100px;
            background-color: purple;
            color: #fff;
            margin: 10px;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
        <span>4</span>
        <span>5</span>
    </div>
</body>
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/4837b51525eb48ebad097946d7a3d03c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

##### 2.2.3.4、align-items 设置侧轴上的子元素排列方式(单行)

该属性是控制子项在侧轴（默认是y轴）上的排列方式 在子项为单项（**单行**）的时候使用

| 属性值         | 说明                       |
| -------------- | -------------------------- |
| **flex-start** | **从上到下**               |
| flex-end       | 从下到上                   |
| **center**     | **挤在一起居中(垂直居中)** |
| **stretch**    | **拉伸(默认值)**           |

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            display: flex;
            width: 800px;
            height: 400px;
            background-color: pink;
            /* 主轴是 y 轴 column */
            flex-direction: column;
            /* 设置主轴上的子元素居中 */
            justify-content: center;
            /* 设置侧轴上的子元素居中 */
            align-items: center;
           
        }
        
        div span {
            width: 150px;
            height: 100px;
            background-color: purple;
            color: #fff;
            margin: 10px;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
    </div>
</body>

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/06f471dc501c4557ac69e9f0679c1f73.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

##### 2.2.3.5、align-content 设置侧轴上的子元素的排列方式(多行)

设置子项在侧轴上的排列方式 并且只能用于子项出现 **换行** 的情况（多行），在单行下是没有效果的。

| 属性值            | 说明                                       |
| ----------------- | ------------------------------------------ |
| **flex-start**    | **默认值在侧轴的头部开始排列**             |
| flex-end          | 在侧轴的尾部开始排列                       |
| **center**        | **在侧轴中间显示**                         |
| **space-around**  | **子项在侧轴平分剩余空间**                 |
| **space-between** | **子项在侧轴先分布在两头，再平分剩余空间** |
| **stretch**       | **设置子项元素高度平分父元素高度**         |

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            display: flex;
            width: 800px;
            height: 400px;
            background-color: pink;
            /* 默认主轴是 x 轴 */
            /* 换行 */
            flex-wrap: wrap;
            /* 因为有了换行，此时我们侧轴上控制子元素的对齐方式我们用 align-content */
            
            /* align-content: flex-start; */
            /* align-content: center; */
            /* align-content: space-between; */
            align-content: space-around;
        }
        
        div span {
            width: 150px;
            height: 100px;
            background-color: purple;
            color: #fff;
            margin: 10px;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
        <span>4</span>
        <span>5</span>
        <span>6</span>
    </div>
</body>

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/27eee5f656584ac9afc8cbaf1c7021d0.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

##### 2.2.3.6、align-content 和 align-items 区别

- align-items 适用于单行情况下， 只有上对齐、下对齐、居中和 拉伸
- align-content 适应于换行（多行）的情况下（单行情况下无效）， 可以设置 上对齐、 下对齐、居中、拉伸以及平均分配剩余空间等属性值。
- 总结就是单行找 align-items 多行找 align-content

![在这里插入图片描述](https://img-blog.csdnimg.cn/480258f6f7254d57ad0de8720a68705c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

### 2.2.4、flex-flow

flex-flow 属性是 flex-direction 和 flex-wrap 属性的复合属性

```
flex-flow: row wrap;
```

- lex-direction：设置主轴的方向
- justify-content：设置主轴上的子元素排列方式
- flex-wrap：设置子元素是否换行
- align-content：设置侧轴上的子元素的排列方式（多行）
- align-items：设置侧轴上的子元素排列方式（单行）
- flex-flow：复合属性，相当于同时设置了 flex-direction 和 flex-wrap

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            display: flex;
            width: 600px;
            height: 300px;
            background-color: pink;
            /* flex-direction: column;
            flex-wrap: wrap; */
            /* 把设置主轴方向和是否换行（换列）简写 */
            flex-flow: column wrap;
        }
        
        div span {
            width: 150px;
            height: 100px;
            background-color: purple;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
        <span>4</span>
        <span>5</span>
    </div>
</body>

```

## 2.3、flex布局子项常见属性

- flex 子项目占的份数
- align-self 控制子项自己在侧轴的排列方式
- order属性定义子项的排列顺序（前后顺序）

### 2.3.1、flex属性

flex 属性定义子项目**分配剩余空间**，用flex来表示占多少份数。

![在这里插入图片描述](https://img-blog.csdnimg.cn/dc679b96741d476e97bb3cb7f7f41d68.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

```
.item {
    flex: <number>;	/* default 0*/
}

```

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        section {
            display: flex;
            width: 60%;
            height: 150px;
            background-color: pink;
            margin: 0 auto;
        }
        
        section div:nth-child(1) {
            width: 100px;
            height: 150px;
            background-color: red;
        }
        
        section div:nth-child(2) {
            flex: 1;
            /*可以用这个属性实现圣杯布局*/
            background-color: green;
        }
        
        section div:nth-child(3) {
            width: 100px;
            height: 150px;
            background-color: blue;
        }
        
        p {
            display: flex;
            width: 60%;
            height: 150px;
            background-color: pink;
            margin: 100px auto;
        }
        
        p span {
            flex: 1;
        }
    </style>
</head>

<body>
    <section>
        <div></div>
        <div></div>
        <div></div>
    </section>
    <p>
        <span>1</span>
        <span>2</span>
        <span>3</span>
    </p>
</body>

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/0760011e9c554d779ee3fa7d4eb53dfe.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

### 2.3.2、align-self 控制子项自己在侧轴上的排列方式

- align-self 属性允许单个项目有与其他项目不一样的对齐方式，可覆盖 align-items 属性。
- 默认值为 auto，表示继承父元素的 align-items 属性，如果没有父元素，则等同于 stretch。

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            display: flex;
            width: 80%;
            height: 300px;
            background-color: pink;
            /* 让三个子盒子沿着侧轴底侧对齐 */
            /* align-items: flex-end; */
            /* 我们想只让3号盒子下来底侧 */
        }
        
        div span {
            width: 150px;
            height: 100px;
            background-color: purple;
            margin-right: 5px;
        }

        div span:nth-child(3) {
            align-self: flex-end;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
    </div>
</body>

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/963925250d4d41149666f567b550821e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

### 2.3.3、order属性定义项目的排列顺序

数值越小，排列越靠前，默认为0。

注意：和 z-index 不一样。

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            display: flex;
            width: 80%;
            height: 300px;
            background-color: pink;
            /* 让三个子盒子沿着侧轴底侧对齐 */
            /* align-items: flex-end; */
            /* 我们想只让3号盒子下来底侧 */
        }
        
        div span {
            width: 150px;
            height: 100px;
            background-color: purple;
            margin-right: 5px;
        }
        
        div span:nth-child(2) {
            /* 默认是0   -1比0小所以在前面  */
            order: -1;
        }
        
        div span:nth-child(3) {
            align-self: flex-end;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
    </div>
</body>

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/7a36164244a646cdae65f5ef6f58efba.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

## 2.4、背景颜色渐变

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            width: 600px;
            height: 200px;
            /* 背景渐变必须添加浏览器私有前缀 */
            /* background: -webkit-linear-gradient(left, red, blue); */
            /* background: -webkit-linear-gradient(red, blue); */
            background: -webkit-linear-gradient(top left, red, blue);
        }
    </style>
</head>

<body>
    <div></div>
</body>

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/974fa15e13cb47f0bc7a265d59f2b33c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

## 2.5、rem适配布局

我们来看几个问题：

1. 页面布局**文字**能否随着屏幕大小变化而变化？
2. 流式布局和flex布局主要针对于宽度布局，那**高度**如何设置？
3. 怎么样让屏幕发生变化的时候元素高度和宽度等比例缩放？

### 2.5.1、rem基础

- rem (root em)是一个相对单位，类似于em，em是父元素字体大小。
  - em 是相对与父元素的文字大小
- 不同的是**rem的基准是相对于html元素的字体**大小。
  - 比如，根元素（html）设置font-size=12px; 非根元素设置width:2rem; 则换成px表示就是24px
  - rem的优势：**父元素文字大小可能不一致， 但是整个页面只有一个html，可以很好来控制整个页面的元素大小**


```html
    <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        html {
            font-size: 12px;
        }
    div {
        font-size: 12px;
        width: 15rem;
        height: 15rem;
        background-color: purple;
    }
    
    p {
        /* 1. em相对于父元素 的字体大小来说的 */
        /* width: 10em;
        height: 10em; */
        /* 2. rem 相对于 html元素 字体大小来说的 */
        width: 10rem;
        height: 10rem;
        background-color: pink;
        /* 3.rem的优点就是可以通过修改html里面的文字大小来改变页面中元素的大小可以整体控制 */
    }
</style>
</head>

<body>
    <div>
        <p></p>
    </div>

</body>
```
![image-20220309192135446](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220309192135446.png)

### 2.5.2、媒体查询

媒体查询（Media Query）是CSS3新语法。

- 使用 @media 查询，可以针对不同的媒体类型定义不同的样式
- @media 可以针对不同的屏幕尺寸设置不同的样式
- 当你重置浏览器大小的过程中，页面也会根据浏览器的宽度和高度重新渲染页面
- 目前针对很多苹果手机、Android手机，平板等设备都用得到多媒体查询

语法如下：

```css
@media mediatype and|not|only(media feature){
    CSS-code
}
```

- 
  用 @media 开头 注意@符号
- mediatype 媒体类型
- 关键字 and not only
- media feature 媒体特性 必须有小括号包含


```html
    <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        /* 这句话的意思就是： 在我们屏幕上 并且 最大的宽度是 800像素 设置我们想要的样式 */
        /* max-width 小于等于800 */
        /* 媒体查询可以根据不同的屏幕尺寸在改变不同的样式 */
    @media screen and (max-width: 800px) {
        body {
            background-color: pink;
        }
    }
    
    @media screen and (max-width: 500px) {
        body {
            background-color: purple;
        }
    }
</style>
<head>
```

上面代码的意思是在我们屏幕上页面处于 500px-800px 之间，页面背景颜色显示为 pink 色。页面小于 500px，背景颜色显示为 purple 色

#### 2.5.2.1、mediatype查询类型

将不同的终端设备划分成不同的类型，称为媒体类型

| 值        | 解释说明                               |
| --------- | -------------------------------------- |
| all       | 用于所有设备                           |
| print     | 用于打印机和打印预览                   |
| **scree** | **用于电脑屏幕、平板电脑、智能手机等** |

#### 2.5.2.2、关键字

关键字将媒体类型或多个媒体特性连接到一起做为媒体查询的条件。

- and：可以将多个媒体特性连接到一起，相当于“且”的意思。
- not：排除某个媒体类型，相当于“非”的意思，可以省略。
- only：指定某个特定的媒体类型，可以省略。

#### 2.5.2.3、媒体特性

每种媒体类型都具体各自不同的特性，根据不同媒体类型的媒体特性设置不同的展示风格。我们暂且了解三个。注意他们要加小括号包含。

| 值        | 解释                               |
| --------- | ---------------------------------- |
| width     | 定义输出设备中页面可见区域的宽度   |
| min-width | 定义输出设备中页面最小可见区域宽度 |
| max-width | 定义输出设备中页面最大可见区域宽度 |

注意： 为了防止混乱，媒体查询我们要按照从小到大或者从大到小的顺序来写,但是我们最喜欢的还是从小到大来写，这样代码更简洁


```html
    <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        /* 1. 媒体查询一般按照从大到小或者 从小到大的顺序来 */
        /* 2. 小于540px 页面的背景颜色变为蓝色 */
    @media screen and (max-width: 539px) {
        body {
            background-color: blue;
        }
    }
    /* 3. 540 ~ 970 我们的页面颜色改为 绿色 */
    /* @media screen and (min-width: 540px) and (max-width: 969px) {
        body {
            background-color: green;
        }
    } */
    
    @media screen and (min-width: 540px) {
        body {
            background-color: green;
        }
    }
    /* 4. 大于等于970 我们页面的颜色改为 红色 */
    
    @media screen and (min-width: 970px) {
        body {
            background-color: red;
        }
    }
    /* 5. screen 还有 and 必须带上不能省略的 */
    /* 6. 我们的数字后面必须跟单位  970px   这个 px 不能省略的 */
</style>
        </head>
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/9ebceb16c2f04d2da6d4425202bf1b86.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

### 2.5.3、媒体查询+rem实现元素动态大小变化

- rem单位是跟着html来走的，有了rem页面元素可以设置不同大小尺寸
- 媒体查询可以根据不同设备宽度来修改样式
- 媒体查询+rem 就可以实现不同设备宽度，实现页面元素大小的动态变化


```html
   <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        /* html {
            font-size: 100px;
        } */
        /* 从小到大的顺序 */
   @media screen and (min-width: 320px) {
        html {
            font-size: 50px;
        }
    }
    
    @media screen and (min-width: 640px) {
        html {
            font-size: 100px;
        }
    }
    
    .top {
        height: 1rem;
        font-size: .5rem;
        background-color: green;
        color: #fff;
        text-align: center;
        line-height: 1rem;
    }
</style>
       </head>
<body>
    <div class="top">购物车</div>
</body>

```
上述代码的意思是：屏幕尺寸小于320px， div 大小为 0.5*50 = 25px，屏幕尺寸大于 320px 小于 640px， div 大小为 0.5 * 100 = 50px

### 2.5.4、引入资源

- 当样式比较繁多的时候，我们可以针对不同的媒体使用不同 stylesheets（样式表）。
- 原理，就是直接在link中判断设备的尺寸，然后引用不同的css文件。

语法：

```html
<link rel="stylesheet" media="mediatype and|not|only (media feature)" href="mystylesheet.css">
```

```html
<link rel="stylesheet" href="styleA.css" media="screen and (min-width: 400px)">
```

### 2.5.5、Less

CSS 是一门非程序式语言，没有变量、函数、SCOPE（作用域）等概念。

- CSS 需要书写大量看似没有逻辑的代码，CSS 冗余度是比较高的。

- 不方便维护及扩展，不利于复用。
- CSS 没有很好的计算能力

- 非前端开发工程师来讲，往往会因为缺少 CSS 编写经验而很难写出组织良好且易于维护的 CSS 代码项目。

Less （Leaner Style Sheets 的缩写） 是一门 CSS 扩展语言，也成为CSS预处理器。

- 做为 CSS 的一种形式的扩展，它并没有减少 CSS 的功能，而是在现有的 CSS 语法上，为CSS加入程序式语言的特性。

- 它在 CSS 的语法基础之上，引入了变量，Mixin（混入），运算以及函数等功能，大大简化了 CSS 的编写，并且降低了 CSS 的维护成本，就像它的名称所说的那样，Less 可以让我们用更少的代码做更多的事情。

- Less中文网址： http://lesscss.cn/

- Less 是一门 CSS 预处理语言，它扩展了CSS的动态特性。


#### 2.5.5.1、Less安装

![image-20220309190655819](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220309190655819.png)

#### 2.5.5.2、Less变量

![image-20220309190710681](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220309190710681.png)

#### 2.5.5.3、Less编译

我们需要把我们的 less文件，编译生成为css文件，这样我们的html页面才能使用。

我们可以在 vscode 安装 Easy LESS 插件来把 less 文件编译为 css。安装完毕插件，重新加载下 vscode。只要保存一下Less文件，会自动生成CSS文件。

#### 2.5.5.4、Less嵌套



#### 2.5.5.5、Less运算



### 2.5.6、rem适配方案

1. 让一些不能等比自适应的元素，达到当设备尺寸发生改变的时候，等比例适配当前设备。
2. 使用媒体查询根据不同设备按比例设置html的字体大小，然后页面元素使用rem做尺寸单位，当html字体大小变化元素尺寸也会发生变化，从而达到等比缩放的适配。

实际开发中适配方案：

1. 按照设计稿与设备宽度的比例，动态计算并设置 html 根标签的 font-size 大小；（媒体查询）
2. CSS 中，设计稿元素的宽、高、相对位置等取值，按照同等比例换算为 rem 为单位的值；

rem 适配方案技术使用

![在这里插入图片描述](https://img-blog.csdnimg.cn/a0b6ea5dab89442096a4d3595c121dc7.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

#### 2.5.6.1、rem实际开发适配方案一

rem + 媒体查询 + less 技术

![在这里插入图片描述](https://img-blog.csdnimg.cn/2f0494ce7c554a6985ac4f0d0db421e4.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

一般情况下，我们以一套或两套效果图适应大部分的屏幕，放弃极端屏或对其优雅降级，牺牲一些效果。现在基本以750为准。

>  动态设置 html 标签 font-size 大小

1. 假设设计稿是750px
2. 假设我们把整个屏幕划分为15等份（划分标准不一可以是20份也可以是10等份）
3. 每一份作为html字体大小，这里就是50px
4. 那么在320px设备的时候，字体大小为320/15 就是 21.33px
5. 用我们页面元素的大小 除以不同的 html 字体大小会发现他们比例还是相同的
6. 比如我们以 750为标准设计稿
7. 一个100*100像素的页面元素 在 750屏幕下， 就是 100 / 50 转换为rem 是 2rem * 2 rem 比例是 1比1
8. 320屏幕下， html 字体大小为 21.33 则 2rem = 42.66px 此时宽和高都是 42.66 但是 宽和高的比例还是 1比1
9. 但是已经能实现不同屏幕下 页面元素盒子等比例缩放的效果

>  元素大小取值方法

1. 最后的公式： 页面元素的rem值 = 页面元素值（px） / （屏幕宽度 / 划分的份数）
2. 屏幕宽度/划分的份数 就是 html font-size 的大小
3. 或者： 页面元素的rem值 = 页面元素值（px） / html font-size 字体大小

