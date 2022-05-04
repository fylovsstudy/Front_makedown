### 1 CSS三大特性

#### 1.1 层叠性

- **相同选择器**设置**相同的样式**，此时一个样式就会**覆盖**另一个冲突的样式。
- 层叠性主要**解决样式冲突的问题**
- 层叠性原则：
  - 样式冲突，遵循的原则是**就近原则**，哪个样式离结构近，就执行哪个样式。
  - 样式不冲突，不会层叠

#### 1.2 继承性

- CSS中的继承：子标签会继承父标签里面的某些样式
- 主要继承：**文本颜色和字号**等，text-，font-，line-
- 例如大的页面中，给body指定文字的颜色和大小，可以简化代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            color: aqua;
            font-size: 14px;
        }
    </style>
</head>

<body>
    <div>
        <p>啦啦啦啦</p>
    </div>
</body>

</html>
```

![](D:\Typora_makedown\前端面试准备\CSS\CSS-02.assets\image-20220214202214629.png)

##### 行高的继承

行高的特殊写法：

- **body行高1.5这样写法最大的优势就是里面的子元素可以根据自己文字的大小自动调整行高**
- 行高可以跟单位也可以不跟
- 如果子元素没有设置行高，则会继承父元素的行高1.5
- 此时子元素的行高是：当前子元素的文字大小*1.5

```css
 font: 12px/1.5 'Microsoft Yahei';
```

行高的继承

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body {
            color: pink;
            font: 12px/1.5 'Microsoft Yahei';
            /*  行高就是12px的1.5倍*/
        }

        div {
            /* 子元素继承了父元素的行高body，1.5 */
            /* 这个1.5就是当前元素文字大小font-size的1.5 倍 */
            font-size: 14px;
        }
    </style>
</head>

<body>
    <div>粉红色的回忆</div>
    <p>粉红色的回忆</p>
</body>

</html>
```

#### 1.3 优先级

- 当同一个元素指定多个选择器，就会有优先级的产生
- 选择器相同，则执行**层叠性**
- 选择器不同，则按**权重**

| 选择器                   | 权重       |
| ------------------------ | ---------- |
| 继承或者 *               | 0，0，0，0 |
| 元素选择器（标签选择器） | 0，0，0，1 |
| 类选择器，伪类选择器     | 0，0，1，0 |
| ID选择器                 | 0，1，0，0 |
| 行内样式style=""         | 1，0，0，0 |
| ！important重要的        | 无穷大     |

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            color: pink !important;
        }

        .smile {
            color: red;
        }

        #demo {
            color: antiquewhite;
        }
    </style>
</head>

<body>
    <div class="smile" id="demo">
        你笑起来真好看
    </div>
</body>

</html>
```

- 等级判断是从左到右，如果某一位数值相同，则判断下一位数值

##### 关于继承的特殊性

- **继承的权重是0**
- 权重可以叠加，**但是永远不会有进位**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #demo {
            color: pink;
        }

        /*虽然id选择器的优先级高于标签选择器，但是p是通过继承得到的id选择器样式，继承的优先级为0，比标签选择器小，所以按标签选择器的颜色红色显示  */
        /* 所以以后看标签到底执行哪个样式，就先看这个标签有没有被单独选出来 */
        p {
            color: red;
        }

        /* a链接浏览器默认指定一个样式  蓝色的 有下划线 */
        a {
            color: green;
        }
    </style>
</head>

<body>
    <div id="demo">
        <p>
            啦啦啦啦啊
        </p>
    </div>
    <a href="#">我是单独的样式</a>
</body>

</html>
```

##### 权重的叠加

```html
<head>
<style>
     li {
        color:green;
     }
/* li 的权重是 0,0,0,1  */
     ul li{
        color :red;
     }
/* 复合选择器权重叠加，ul li权重 0,0,0,1 + 0,0,0,1 =0,0,0,2 */
.nav li{
    color:pink;
}
/*  .nav li 权重 0,0,1,0 + 0,0,0,1 = 0,0,1,1 */
<style>
</head>
<body>
    <ul  class="nav">
          <li>大猪蹄子</li>
          <li>大肘子</li>
          <li>猪尾巴</li>
      
    </ul>
</body>
```

1. `div ul li`----------> 0,0,0,3
2. `.nav ul li` -------------->0,0,1,2
3. `a:hover` ---------------->0,0,1,1 /* 伪类选择器*/
4. `.nav a`-------------------->0,0,1,1

##### 权重练习

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        /* .nav {
            color: pink
        }

        li {
            color: red;
        }
        继承的权重是0,显示红色
        */

        .nav li {
            color: red;
        }

        .nav .pink {
            color: pink;
        }
    </style>
</head>

<body>
    <ul class="nav">
        <li class="pink">1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
    </ul>
</body>

</html>
```

### 2 CSS 盒子模型

页面布局要学习三大核心

- **盒子模型**
- **浮动**
- **定位**

盒子模型的组成：

- `border(边框)`
- `content(内容)`
- `padding(内边距)`
- `margin(外边距)`

![img](https://img-blog.csdnimg.cn/4d812f91aa1b4c639298a6460357b775.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

#### 2.1 看透网页布局的本质

网页布局的过程：

1. 先准备好相关网页元素，网页元素基本都是盒子box
2. 利用css 设置好盒子样式，然后摆放到相应的位置
3. 往盒子里面装内容

网页布局的核心本质：就是利用CSS摆盒子

#### 2.2 盒子模型的组成

所谓盒子模型：就是把HTML页面中的布局元素看做成一个矩形的盒子，也是一个承装内容的容器。

CSS盒子模型本质上是一个盒子，封装周围的HTML元素，它包括：边框，外边距，内边距和实际内容。

![image-20220214213254781](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220214213254781.png)

#### 2.3 边框（border）

- CSS 边框属性允许你指定一个元素边框的样式和颜色
- 边框由三部分组成：**边框宽度（粗细） 边框样式 边框颜色**

```
border : borde-width || border-style || border-color
```

| 属性         | 作用                   |
| ------------ | ---------------------- |
| border-width | 定义边框粗细，单位是px |
| border-style | 边框的样式             |
| border-color | 边框颜色               |

##### 2.3.1、border-style

边框样式 border-style可以设置如下值：

1. `none`:没有边框即忽略所有边框的宽度（默认值）
2. `solid` :边框为单实线（最为常用的）
3. `dashed`: 边框为虚线
4. `dotted`: 边框为点线

边框简写：没有顺序

```css
border : 1px soilid red;
```

边框分开写法：

```css
/*只设定上边框，其余同理 top bottom left right*/
border-top: 1px solid red;
```

给一个500*500的盒子，设置上边框是粉红色

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            width: 500px;
            height: 500px;
            /* border-top: 1px solid pink;
            border: 1px solid red;
            这样写不对   就近原则 */
            border: 1px solid red;
            border-top: 1px solid pink;
        }
    </style>
</head>
<body>
    <div></div>
</body>
</html>
```

##### 2.3.2、border-collapse表格细线边框

- border-collapse 属性控制浏览器绘制表格边框的方式，它控制相邻单元格的边框
- `border-coppapse` 表格的细线边框

```css
border-collapse : collapse;
```

- 表示相邻边框合并在一起
- collapse 单词是合并的意思

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        table,
        td,
        th {
            border: 1px solid black;
            /* 合并相邻的边框 */
            border-collapse: collapse;
        }
    </style>
</head>

<body>
    <table align="center" cellspacing="0">
        <thead>
            <tr>
                <th>1</th>
                <th>1</th>
                <th>1</th>
                <th>1</th>
                <th>1</th>
            </tr>
            <tr>
                <td>12345</td>
                <td>12345</td>
                <td>12345</td>
                <td>12345</td>
                <td>12345</td>
            </tr>
            <tr>
                <td>67890</td>
                <td>67890</td>
                <td>67890</td>
                <td>67890</td>
                <td>67890</td>
            </tr>
        </thead>
    </table>
</body>

</html>
```

##### 2.3.3、边框会影响盒子实际大小

边框会额外增加盒子的实际大小，因此我们有两种方案解决：

1. 测量盒子大小的时候，不量边框
2. 如果测量的时候包含了边框，则需要 width/height 减去边框宽度

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            width: 200px;
            height: 300px;
            background-color: pink;
            border: 10px solid black;
             /* 加上了这一句整个盒子宽度就会变成220px */
        }
    </style>
</head>
<body>
    <div>
    </div>
</body>
</html>
```

#### 2.4 内边距padding

padding 属性用于设置**内边距**,**即盒子边框与内容之间的距离**

|      属性      |   作用   |
| :------------: | :------: |
|  padding-left  | 左内边距 |
| padding-right  | 右内边距 |
|  padding -top  | 上内边距 |
| padding-bottom | 下内边距 |

- padding属性(简写属性)可以有一到四个值

|          值的个数           |                           表达意思                           |
| :-------------------------: | :----------------------------------------------------------: |
|       padding : 5px;        |            1个值，代表**上下左右**都有5像素内边距            |
|     padding :5px 10px;      |       2个值，代表上下内边距是5像素，左右内边距是10像素       |
|   padding: 5px 10px 20px;   |  3个值，代表上内边距5像素，左右内边距10像素，下内边距20像素  |
| padding :5px 10px 20px 30px | **4个值，上是5像素，右是10像素，下20像素，左是30像素，顺时针** |

以上四种情况，我们实际开发都会遇到。

##### 2.4.1 影响盒子大小

> padding会影响盒子大小的情况

当我们给盒子指定 padding 值之后，发生了2件事情：

1. 内容和边框有了距离，添加了内边距

2. padding影响了盒子实际大小

   - **也就是说，如果盒子已经有了宽度和高度，此时再指定内边框，会撑大盒子**

   - 解决方案：

     **如果保证盒子跟效果图大小保持一致，则让 width/height 减去多出来的内边距大小即可**,例如:如果需要保证盒子的宽高为200和300,则把width(200)和height(300)减去padding的值,得到新的width和height

但是，有时候 padding 影响盒子是有好处的，比如我们要做导航：

![在这里插入图片描述](https://img-blog.csdnimg.cn/abd79f7b40c8482a8140fd74b7149040.png#pic_center)

因为每个导航栏里面的字数不一样多,我们可以不用给每个盒子宽度了,直接给 padding 最合适.

如果是设置width和height则会导致文字和边框之间的间隔不统一,影响美观,如下图所示:

![image-20220217194225196](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220217194225196.png)

```html
!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .nav {
            height: 41px;
            border-top: 3px solid #ff8500;
            border-bottom: 1px solid #edeef0;
            background-color: #fcfcfc;
            line-height: 41px;
        }

        .nav a {
            /* a属于行内元素，没有高度，需要转化为行内块元素 */
            display: inline-block;
            padding: 0 20px;
            font-size: 12px;
            color: #4c4c4c;
            text-decoration: none;
            height: 41px;
        }

        .nav a:hover {
            background-color: #eee;
            color: #ff8500;
        }
    </style>
</head>

<body>
    <div class="nav">
        <a href="#">新浪导航</a>
        <a href="#">手机新浪网</a>
        <a href="#">微博</a>
        <a href="#">客户端</a>
    </div>
</body>
</html>
```

##### 2.4.2 不影响盒子大小

> padding不会影响盒子大小的情况

- **如果盒子本身没有指定width/height属性，则此时padding不会撑开盒子大小**
- 同理,如果孩子和父亲宽高一样,则孩子可以不指定宽高,这样设置padding的时候就不会撑大盒子

#### 2.5 外边距margin

- `margin`（外边距）属性用于设置外边距，即控制**盒子和盒子**之间的距离

|     属性      |   作用   |
| :-----------: | :------: |
|  margin-left  | 左外边距 |
| margin-right  | 右外边距 |
|  margin-top   | 上外边距 |
| margin-bottom | 下外边距 |

margin 简写方式代表的意义跟 padding 完全一致

##### 2.5.1 外边距的典型应用

外边距可以让**块级盒子水平居中**，但是必须满足两个条件

1. 盒子必须制定了宽度(width)
2. 盒子**左右的外边距**都设置为 auto

```css
.header {
    width: 960px;
    margin: 0 auto;
}
```

左右的外边距都设置为 auto 有三种写法：

```css
margin-left: auto; margin-right: auto;
margin: auto;
margin: 0 auto;
```

**注意**：

以上方法是让**块级元素**水平居中，**行内元素或者行内块元素**水平居中给其父元素添加 text-align: center 即可。

```html
<style>
        .header {
            width: 300px;
            height: 200px;
            background-color: pink;
            margin: 0 auto;
            text-align: center;
            /* 行内元素和行内块元素想要水平居中对齐，需要把它的父元素设置text-align center */
        }
    </style>
    <body>
    <div class="header">
        <span>这是行内元素</span>
    </div>
</body>
```

###### ①相邻块元素垂直外边距的合并🔥

当上下相邻的两个块元素（兄弟关系）相遇时，如果上面的元素有下外边距 margin-bottom，下面的元素有上外边距 margin-top ，则他们之间的垂直间距不是 margin-bottom 与 margin-top 之和。取两个值中的较大者这种现象被称为相邻块元素垂直外边距的合并。

<img src="https://img-blog.csdnimg.cn/7718ee0385bf4536b331b7e551b8449b.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center" alt="在这里插入图片描述" style="zoom:50%;" />

解决方案：

**尽量只给一个盒子添加 margin 值**

###### ②嵌套块元素垂直外边距的塌陷🔥

出现的条件:父子盒子嵌套,子盒子有margin-top.

对于两个嵌套关系（父子关系）的块元素，父元素有上外边距同时子元素也有上外边距，此时父元素会塌陷较大的外边距值

<img src="https://img-blog.csdnimg.cn/0bc4b88590cd435bb8376893c2fe542e.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center" alt="在这里插入图片描述" style="zoom:50%;" />

解决方案：

1. 可以为父元素定义上边框

   ```css
   border-top: 2px solid transparent;
   ```

2. 可以为父元素定义上内边距

   ```css
   padding: 1px;
   ```

3. **可以为父元素添加 overflow: hidden**

   ```css
   overflow:hidden;
   ```

还有其他方法，比如浮动、固定、绝对定位的盒子不会有塌陷问题。后面会进行总结。

###### ③清除内外边距🔥

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220217213759639.png" alt="image-20220217213759639" style="zoom:50%;" />

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220217213543720.png" alt="image-20220217213543720" style="zoom:50%;" />



网页元素很多都带有默认的内外边距，而且不同浏览器默认的也不一致。因此我们在布局前，首先要清除下网页元素的内外边距。

```css
* {
    padding: 0;
    margin: 0;
}
```

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220217213905691.png" alt="image-20220217213905691" style="zoom:50%;" />

注意：**行内元素为了照顾兼容性，尽量只设置左右内外边距，不要设置上下内外边距。但是转换为块级和行内块元素就可以了**

#### 2.6 综合案例

##### 2.6.1 小米

- 什么时候用margin padding设置距离
- 让块级盒子水平居中
- 子元素怎么设置和父级元素一样宽
- 什么时候padding会撑开盒子,什么时候不会

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220217222135694.png" alt="image-20220217222135694" style="zoom:67%;" />

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0px;
            padding: 0px;
        }

        body {
            background-color: #f5f5f5;
        }

        .box {
            width: 298px;
            height: 415px;
            background-color: #fff;
            /* 让块级盒子水平居中对齐 */
            margin: 100px auto;
        }

        .box img {
            /* 和父亲一样宽 */
            width: 100%;
        }

        .box .review {
            padding: 0 28px;
            /* 因为这个段落没有width属性，所以padding不会撑开盒子宽度 */
            height: 70px;
            font-size: 14px;
            margin-top: 30px;
        }

        .praise {
            font-size: 12px;
            color: #b0b0b0;
            margin-top: 20px;
            padding: 0 28px;
        }

        .info {
            margin-top: 15px;
            font-size: 14px;
            padding: 0 28px;
        }

        .info h4 {
            display: inline-block;
            font-weight: 400;
        }

        .info span {
            color: #ff7400;
        }

        .info em {
            font-style: normal;
            color: #b0b0b0;
            margin: 0 6px 0 15px;
        }

        a {
            text-decoration: none;
            color: black;
        }
    </style>
</head>

<body>
    <div class="box">
        <img src="picture.png" alt="">
        <p class="review">快递牛，快递牛，快递牛，快递牛，快递牛，快递牛</p>
        <div class="praise">来自12344567评价:</div>
        <div class="info">
            <h4><a href="#">Redmi 蓝牙耳机...</a></h4>
            <em>|</em>
            <span>99.9元</span>
        </div>
    </div>
</body>

</html>
```

**总结**

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220217222606856.png" alt="image-20220217222606856" style="zoom:80%;" />

##### 2.6.2 新闻快报

- li怎么出去小圆点

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            /* 清除内外边距 */
            margin: 0px;
            padding: 0px;
        }

        .box {
            width: 248px;
            height: 163px;
            border: 1px solid #ccc;
            margin: 100px auto;
        }

        .box h4 {
            height: 32px;
            font-weight: 400px;
            font-size: 14px;
            border-bottom: 1px dotted #ccc;
            line-height: 32px;
            padding-left: 10px;
            /* 这里不能用margin 因为下划线也会有空隙 */
            color: rgb(104, 100, 100);
        }

        ul {
            margin: 5px 20px;
            font-size: 14px;
            color: rgb(104, 100, 100);
        }

        li {
            list-style: none;
            height: 23px;
            line-height: 23px;
            /* li去除前面的小圆点 */
        }

        a {
            text-decoration: none;
            color: rgb(104, 100, 100);
            font-size: 12px;
        }

        a:hover {
            text-decoration: underline;
        }
    </style>
</head>

<body>
    <div class="box">
        <h4>品有够快报</h4>
        <ul>
            <li><a href="#">【特惠】 111</a></li>
            <li><a href="#">【特惠】 222</a></li>
            <li><a href="#">【特惠】 333</a></li>
            <li><a href="#">【特惠】 444</a></li>
            <li><a href="#">【特惠】 555</a></li>
        </ul>
    </div>

</body>

</html>
```

#### 2.7 圆角边框

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220217234341090.png" alt="image-20220217234341090" style="zoom:80%;" />

- 在 CSS3 中，新增了圆角边框样式，这样我们的盒子就可以变圆角了。
- border-radius 属性用于设置元素的外边框圆角。

```css
border-radius:length;
```

radius半径（圆的半径） 原理:(椭）圆与边框的交集形成圆角效果
参数值可以是数值或百分比的形式
如果是正方形，想要设置为一个圆，把数值修改为高度或者宽度的一半即可，或者直接写为50%
如果是一个矩形，设置为高度的一半就可以
该属性是一个简写属性，可以跟四个值，分别代表左上角，右上角，右下角，左下角

```css
border-top-left-radius:
border-top-right-radius:
border-bottom-right-radius:
border-bottom-left-radius:
```

**设置圆形**

```css
/* 设置圆形 */
border-radius: 150px;
border-radius: 50%;
```

**设置圆角矩形**

```css
 width: 500px;
 height: 200px;
 background-color: pink;
 /* 设置圆形矩形:设置为高度的一半*/
 border-radius: 100px;
```

#### 2.8 盒子阴影

##### 2.8.1 设置

CSS3 中新增了盒子阴影，我们可以使用 box-shadow 属性为盒子添加阴影。

```css
box-shadow: h-shadow v-shadow blur spread color inset;
```

| 值       | 描述                                   |
| -------- | -------------------------------------- |
| h-shadow | 必需。水平阴影的位置，允许负值         |
| v-shadow | 必需。垂直阴影的位置，允许负值         |
| blur     | 可选。模糊距离。                       |
| spread   | 可选，阴影的尺寸。                     |
| color    | 可选，阴影的颜色。                     |
| inset    | 可选，将外部阴影（outset）改为内部阴影 |

- 模糊距离：影子的虚实
- 阴影尺寸：影子的大小

**注意：**

1. 默认的是外阴影（outset），但是不可以在后面写这个单词，否则导致阴影无效
2. **盒子阴影不占用空间，不会影响其他盒子排列**

##### 2.8.2 文字阴影

在 CSS3 中，我们可以使用 text-shadow 属性将阴影应用于文本。

```css
text-shadow: h-shadow v-shadow blur color
```

|    值    |              描述              |
| :------: | :----------------------------: |
| h-shadow | 必需。水平阴影的位置，允许负值 |
| v-shadow | 必需。垂直阴影的位置，允许负值 |
|   blur   |         可选。模糊距离         |
|  color   |       可选，阴影的颜色。       |

### 3 传统网页布局的三种方式🔥

网页布局的本质➡用 CSS 来摆放盒子。 把盒子摆放到相应位置

CSS 提供了三种传统布局方式：

- 普通流（标准流）
- 浮动
- 定位

#### 3.1标准流

所谓的标准流，就是标签按照规定好默认方式排列

1. 块级元素会独占一行，从上向下顺序排列。

   常用元素：div、hr、p、h1~h6、ul、ol、dl、form、table

2. 行内元素会按照顺序，从左到右顺序排列，碰到父元素边缘则自动换行。
   常用元素：span、a、i、em 等

以上都是标准流布局，我们前面学习的就是标准流，标准流是最基本的布局方式。

这三种布局方式都是用来摆放盒子的，盒子摆放到合适位置，布局自然就完成了。

注意：实际开发中，一个页面基本都包含了这三种布局方式（后面移动端学习新的布局方式） 。

#### 3.2 浮动

1. 提问：如何让多个块级盒子(div)水平排列成一行？

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220308194721299.png" alt="image-20220308194721299" style="zoom:67%;" />

比较难，虽然转换为行内块元素可以实现一行显示**，但是他们之间会有大的空白缝隙**，很难控制。

2. 提问：如何实现两个盒子的左右对齐？

<img src="https://img-blog.csdnimg.cn/c6c08da2c7684a629aca15f1d993a609.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center" alt="img" style="zoom:67%;" />

总结： 有很多的布局效果，标准流没有办法完成，此时就可以利用浮动完成布局。 因为浮动可以改变元素标签默认的排列方式

##### 3.2.1 浮动的典型应用

- 浮动最典型的应用：**可以让多个块级元素一行内排列显示。**
- 网页布局第一准则：**多个块级元素纵向排列找标准流，多个块级元素横向排列找浮动。**

>  什么是浮动？

- `float`属性用于创建浮动框，将其移动到一边，直到左边缘或右边缘触及包含块或另一个浮动框的边缘

语法：

```
选择器 {
    float: 属性值;
}
```

| 属性值 | 描述         |
| ------ | ------------ |
| none   | 元素不浮动   |
| left   | 元素向左浮动 |
| right  | 元素向右浮动 |

- 网页布局的第一准则：**多个块级元素纵向排列找标准流，多个块级元素横向排列找浮动**
- 网页布局第二准则：**先设置盒子大小，之后设置盒子的位置。**

##### 3.2.2 浮动的特性(重点)

设置了浮动（float）的元素的最重要的特性：

1. **脱标**：浮动元素会脱离标准流

- 浮动的盒子**不再保留原先的位置**

![在这里插入图片描述](https://img-blog.csdnimg.cn/c6416c483c96451092a80ada9785b347.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

2. 如果多个盒子都设置了浮动，则它们会按照属性值**一行内显示并且顶端对齐排列**

![在这里插入图片描述](https://img-blog.csdnimg.cn/8dd268845ede45a8bdedb52bf8bb0914.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

- 浮动的元素是相互贴靠在一起的（**不会有缝隙**），如果父级宽度装不下这些浮动的盒子，多出的盒子会另起一行对齐。

3. 浮动元素会具有行内块元素特性

任何元素都可以浮动。不管原先是什么模式的元素，添加浮动之后都具有**行内块元素**相似的特性。

- 如果块级盒子没有设置宽度，默认宽度和父级一样宽，但是添加浮动后，它的大小根据内容来决定
- 如果行内元素有了浮动，则不需要转换块级\行内块元素就可以直接给高度和宽度
- 浮动的盒子中间是没有缝隙的，是紧挨着一起的

##### 3.2.3、浮动元素经常和标准流父级搭配使用

为了约束浮动元素位置, 我们网页布局一般采取的策略是:

**先用标准流的父元素排列上下位置，之后内部子元素采取浮动排列左右位置**

![在这里插入图片描述](https://img-blog.csdnimg.cn/1eb22d8b2c8543d19d0078f8acc2575a.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

##### 3.2.4、浮动的注意点🔥

- 先用标准流的父元素排列上下位置，之后内部子元素采取浮动排列左右位置
- 一个元素浮动了，理论上其余兄弟元素也要浮动
  - 一个盒子里面有多个子盒子，如果其中一个盒子浮动了，那么其他兄弟也应该浮动
- 浮动的盒子只会影响浮动盒子后面的标准流，不会影响前面的标准流

##### 3.2.5、清除浮动

我们前面浮动元素有一个标准流的父元素, 他们有一个共同的特点,

都是有高度的.但是, 所有的父盒子都必须有高度吗?

理想中的状态, 让子盒子撑开父亲. 有多少孩子,我父盒子就有多高.

但是不给父盒子高度会有问题吗?..…

> 为什么要清除浮动

- 由于父级盒子很多情况下，不方便给高度，但是子盒子浮动又不占有位置，最后父级盒子高度为0时，就会影响下面的标准流盒子。

![在这里插入图片描述](https://img-blog.csdnimg.cn/7ae44f5681f549a99c1b7d1f45e5205b.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

- 由于浮动元素不再占用原文档流的位置，所以它会对后面的元素排版产生影响
- 理想中的状态，让子盒子撑开父亲，有多少孩子，我父盒子就有多高

##### 3.2.6、清除浮动的本质

- 清除浮动的本质是**清除浮动元素造成的影响**
- 如果父盒子本身有高度，**则不需要清除浮动**
- 清除浮动之后，父级就会根据浮动的子盒子自动检测高度，父级有了高度，就不会影响下面的标准流了。

语法：

```
选择器 {
    clear: 属性值;
}
```

| 属性值 | 描述                                     |
| ------ | ---------------------------------------- |
| left   | 不允许左侧有浮动元素(清除左侧浮动的影响) |
| right  | 不允许右侧有浮动元素(清除右侧浮动的影响) |
| both   | 同时清除左右两侧浮动的影响               |

- 我们实际工作中，几乎只用`clear:both`
- 清除浮动的策略是：**闭合浮动**
- 只让浮动在父盒子内部影响，不影响父盒子外面的其他盒子。

##### 3.2.7、清除浮动的方法

1. **额外标签法**也称为隔墙法，是W3C推荐的做法
2. 父级添加 overflow 属性
3. 父级添加 after 伪元素
4. 父级添加双伪元素

###### ①额外标签法

- 额外标签法会在浮动元素末尾添加一个空的标签,例如：
- 例如<div style="clear:both"></div>，或者其他标签（如</br>等）

- 注意：要求这个新的空标签必须是块级元素

- 优点：通俗易懂，书写方便

- 缺点：添加许多无意义的标签，结构化较差

- 实际工作可能会遇到,但是不常用

###### ②overflow

- 可以给父级添加`overflow`属性，将其属性值设置为`hidden`,`auto`或`scroll`
- 优点：代码简洁
- 缺点：无法显示溢出的部分

###### ③after伪元素法

:after 方式是额外标签法的升级版。也是给父元素添加

```css
.clearfix:after {
    content: "";
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
}
.clearfix {
      /* IE6,7专有*/
      *zoom : 1; 
}
```

- 优点：没有增加标签，结构更简单
- 缺点：需要照顾低版本浏览器
- 代表网站：百度、淘宝、网易等

###### ④双伪元素

- 也是给父元素添加

```css
.clearfix:before,.clearfix:after{
   content:"";
   display:table;
}
.clearfix:after {
     clear:both;
}
.clearfix {
  *zoom:1;
}
```

- 优点：代码更简洁
- 缺点：需要照顾低版本浏览器
- 代表网站：小米、腾讯等

##### 3.2.8、浮动总结🔥

> 为什么需要清除浮动？

①：父级没高度

②：子盒子浮动了

③：影响下面布局了，我们就应该清除浮动了。

| 清除浮动方式         | 优点               | 缺点                               |
| -------------------- | ------------------ | ---------------------------------- |
| 额外标签法(隔墙法)   | 通俗易懂，书写方便 | 添加许多无意义的标签，结构化较差   |
| 父级overflow:hidden; | 书写简单           | 溢出隐藏                           |
| 父级after伪元素      | 结构语义化正确     | 由于IE6-7不支持：after，兼容性问题 |
| 父级双伪元素         | 结构语义化正确     | 由于IE6-7不支持：after，兼容性问题 |

#### 3.3 定位🔥

提问：以下情况使用标准流或者浮动能实现吗？

1. 某个元素可以自由的在一个盒子内移动位置，并且压住其他盒子。
2. 当我们滚动窗口的时候，盒子是固定屏幕某个位置的。

以上效果，标准流或浮动都无法快速实现，此时需要定位来实现

- 浮动可以让多个块级盒子一行没有缝隙的排列显示，经常用于横向排列盒子
- 定位则是可以让盒子自由的在某个盒子内移动位置或固定屏幕中某个位置，并且可以压住其他盒子
- 定位：将盒子定在某一个位置，所以定位也是在摆放盒子，按照定位的方式移动盒子

##### 3.3.1、定位的组成🔥

定位 = 定位模式 +边偏移

- **定位模式用于指定一个元素在文档中的定位方式**
- **边偏移则决定了该元素的最终位置**

> 定位模式

- 定位模式决定元素的定位方式 ，它通过 CSS 的 position 属性来设置，其值可以分为四个

| 值       | 语义     |
| -------- | -------- |
| static   | 静态定位 |
| relative | 相对定位 |
| absolute | 绝对定位 |
| fixed    | 固定定位 |

> 边偏移

边偏移就是定位的盒子移动到最终位置。

| 边偏移属性 | 示例         | 描述                                                 |
| ---------- | ------------ | ---------------------------------------------------- |
| top        | top: 80px    | 顶端偏移量，定义元素相对于其父元素的**上边线的距离** |
| bottom     | bottom: 80px | 底部偏移量，定义元素相对于其父元素的**下边线的距离** |
| right      | right: 80px  | 右侧偏移量，定义元素相对于其父元素**右边线的距离**   |
| left       | left: 80px   | 左侧偏移量，定义元素相对于其父元素**左边线的距离**   |

##### 3.3.2、静态定位static（了解）

- 静态定位是元素的**默认定位方式，无定位**的意思
- 静态定位按照标准流特性摆放位置，它没有边偏移

```
选择器 {
	position: static;
}
```

##### 3.3.3、相对定位relative🔥

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220308223957661.png" alt="image-20220308223957661" style="zoom:67%;" />

- 相对定位是元素在移动位置的时候，是相对于它原来的位置来说的

- 特点：

  - 它是相对于自己原来的位置来移动的（移动位置的时候参照点是自己原来的位置）

  - 原来在标准流的位置继续占有，后面的盒子仍然以标准流的方式对待。（不脱标，继续保留原来位置）

  - 因此，相对定位并没有脱标，它最典型的应用是给绝对定位当爹的。

##### 3.3.4、绝对定位absolute🔥

- 绝对定位是元素在移动位置的时候，是相对于它的祖先元素来说的

- 特点：

  - 如果没有祖先元素，或者祖先元素没定位，则以浏览器为准进行定位(Document 文档)

  - 如果祖先元素父级有定位(相对、绝对、固定定位)，则以最近一级的有定位祖先元素为参考点移动位置

  - 绝对定位不再占用原先的位置（脱标）

所以绝对定位是脱离标准流的

###### ①绝对定位盒子水平居中🔥

- 加了绝对定位的盒子不能通过`margin: 0 auto`水平居中
- 但是可以通过以下计算方法实现水平和垂直居中

```js
.box {
    position: absolute;
    /* 1.left走50%，父容器宽度的一半 */
    left: 50%;
    /* 2.margin 负值往左边走 自己盒子宽度的一半 */
    margin-left: -xx;
}
```

##### 3.3.5、子绝父相🔥

意思：子级使用绝对定位，父级则需要相对定位

①：子级绝对定位，不会占有位置，可以放到父盒子里面的任何一个地方，不会影响其他的兄弟盒子。

②：父盒子需要加定位限制子盒子在父盒子内显示

③：父盒子布局时，需要占有位置，因此父亲只能是相对定位。

总结：因为父级需要占有位置，因此是相对定位，子盒子不要占有位置，则是绝对定位

##### 3.3.6、固定定位fixed

**固定定位**是元素**固定于浏览器的可视区的位置**

主要使用场景： 可以在浏览器页面滚动时元素的位置不会改变

- 特点🔥：
  - 以浏览器的可视窗口为参照点移动元素
  - 跟父元素没有任何关系
  - 不随滚动条滚动
  - 固定定位**不再占有原先的位置**(脱标)

固定定位也是脱标的，其实固定定位也可以看做是一种特殊的绝对定位。

###### 👉固定定位小技巧🔥

固定定位小技巧： 固定在版心右侧位置

小算法：

1. 让固定定位的盒子 left: 50%. 走到浏览器可视区（也可以看做版心） 的一半位置。
2. 让固定定位的盒子 margin-left: 版心宽度的一半距离。 多走 版心宽度的一半位置

就可以让固定定位的盒子贴着版心右侧对齐了。

```css
.box {
    position: absolute;
    /* 1.left走50%，父容器宽度的一半 */
    left: 50%;
    /* 2.margin 负值往左边走 自己盒子宽度的一半 */
    margin-left: -xx;
}
```

- 注意：绝对定位和固定定位不可以通过margin：0 auto设置水平居中。但是相对定位可以，因为它没有脱离标准流

##### 3. 3.7、粘性定位sticky(了解)

- 特点：
  - 以浏览器的可视窗口为参照点移动元素（固定定位特点）
  - 粘性**定位占有原先的位置**（相对定位的特点）
  - 必须添加top，left，right，bottom其中一个才有效

跟页面滚动搭配使用。 兼容性较差，IE 不支持。

```css
选择器 {
    position:sticky;  
	top: 10px;
}
```

##### 3.3.8、定位模式总结🔥

| 定位模式          | 是否脱标             | 移动位置         | 是否常用   |
| ----------------- | -------------------- | ---------------- | ---------- |
| static静态定位    | 否                   | 不能使用边偏移   | 很少       |
| 定位模式          | 是否脱标             | 移动位置         | 是否常用   |
| static静态定位    | 否                   | 不能使用边偏移   | 很少       |
| **fixed固定定位** | **是（不占有位置）** | **浏览器可视区** | **常用**   |
| sticky            | 否（占有位置）       | 浏览器可视区     | 当前阶段少 |

- 一定要记住相对定位，固定定位，绝对定位的两个大特点：1.是否占有位置（脱标否）2.以谁为基准点移动
- 重点学会子绝父相（儿子绝对定位，父亲必须相对定位）

##### 3.3.9定位叠放次序z-index🔥

- 在使用定位布局时候，可能会出现盒子重叠的情况
- 此时，可以用 z-index 来控制盒子的前后次序(z轴)

```css
选择器 {
    z-index: 1; 
}
```

1. 数值可以是正整数，负整数或者0，默认是auto，数值越大，盒子越靠上
2. 如果属性值相同，则按照书写顺序，后来居上
3. 数字后面不能加单位
4. **只有定位**的盒子才有 z-index 属性

##### 3.3.10、定位的扩展🔥

✍绝对定位的盒子水平居中
加了绝对定位的盒子不能通过 margin: 0 auto 水平居中，但是可以通过以下计算方法实现水平和垂直居中

①：left: 50%; 让盒子的左侧移动到父级元素的水平中心位置

②：margin-left: -100px; 让盒子向左移动自身宽度的一半

✍绝对定位的盒子垂直居中

①：top: 50%; 

②：margin-top: -100px; 让盒子向上移动自身宽度的一半

✍定位特殊特性
绝对定位和固定定位也和浮动类似。

①：行内元素添加绝对或者固定定位，可以直接设置高度和宽度

②：块级元素添加绝对或者固定定位，如果不给宽度或者高度，默认大小是内容的大小。

✍脱标的盒子不会触发外边距塌陷
浮动元素、绝对定位(固定定位)元素都不会触发外边距合并的问题。

✍绝对定位(固定定位)会完全压住盒子
①：浮动元素不同，只会压住它下面标准流的盒子，但是不会压住下面标准流盒子里面的文字（图片）

②：但是绝对定位（固定定位） 会压住下面标准流所有的内容。

③：浮动之所以不会压住文字，因为浮动产生的目的最初是为了做文字环绕效果的。 文字会围绕浮动元素


#### 3.4 网页布局总结

通过盒子模型，清楚知道大部分html标签是一个盒子

通过CSS浮动、定位 可以让每个盒子排列成为网页

一个完整的网页，是标准流、浮动、定位一起完成布局的，每个都有自己的专门用法

1. 标准流
   可以让盒子上下排列或者左右排列，垂直的块级盒子显示就用标准流布局。

2. 浮动
   可以让多个块级元素一行显示或者左右对齐盒子，多个块级盒子水平显示就用浮动布局。

3. 定位
   定位最大的特点是有层叠的概念，就是可以让多个盒子前后叠压来显示。如果元素自由在某个盒子内移动就用定位布局。

### 4 元素的隐藏与显示🔥

类似网站广告，当我们点击关闭就不见了，但是我们重新刷新页面，会重新出现！

本质：**让一个元素在页面中隐藏或者显示出来**

#### 4.1、display显示隐藏🔥

`display`属性用于设置一个元素应如何显示

```
display: none;  /*隐藏对象*/
display: block; /*除了转换为块级元素之外，同时还有显示元素的意思*/
```

- **display隐藏元素后，不再占有原来的位置**

后面应用及其广泛，搭配 JS 可以做很多的网页特效。

#### 4.2、visibility显示隐藏🔥

`visibility`属性用于指定一个元素应可见还是隐藏

```
visibility: visible; /*元素可视*/
visibility: hidden;  /*元素隐藏*/
```

- **visibility 隐藏元素后，继续占有原来的位置。**
- 如果隐藏元素想要原来位置， 就用 `visibility：hidden`
- 如果隐藏元素不想要原来位置， 就用 `display：none` (用处更多 重点）

#### 4.3、overflow溢出显示隐藏🔥

overflow 属性指定了如果内容溢出一个元素的框（超过其指定高度及宽度） 时，会发生什么。

| 属性值  | 描述                                       |
| ------- | ------------------------------------------ |
| visible | 不剪切内容也不添加滚动条                   |
| hidden  | 不显示超过对象尺寸的内容，超出的部分隐藏掉 |
| scroll  | 不管超出内容否，总是显示滚动条             |
| auto    | 超出自动显示滚动条，不超出不显示滚动条     |

一般情况下，我们都不想让溢出的内容显示出来，因为溢出的部分会影响布局。
但是如果有定位的盒子， 请慎用 overflow:hidden 因为它会隐藏多余的部分。
