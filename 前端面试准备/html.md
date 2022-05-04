### 一 web初识

#### 1 .1认识web

**「网页」**主要是由`文字`、`图像`和`超链接`等元素构成，当然除了这些元素，网页中还可以包括音频、视频以及Flash等。

**「浏览器」**是网页显示、运行的平台。负责读取网页内容，整理讯息，计算网页显示方式并显示页面。

**「浏览器内核」**(排版引擎、解释引擎、渲染引擎)

| 浏览器  |      内核      | 备注                                                         |
| :------ | :------------: | :----------------------------------------------------------- |
| IE      |    Trident     | IE、猎豹安全、360极速浏览器、百度浏览器                      |
| firefox |     Gecko      | 可惜这几年已经没落了，打开速度慢、升级频繁、猪一样的队友flash、神一样的对手chrome。 |
| Safari  |     webkit     | 现在很多人错误地把 webkit 叫做 chrome内核（即使 chrome内核已经是 blink 了）。苹果感觉像被别人抢了媳妇，都哭晕在厕所里面了。 |
| chrome  | Chromium/Blink | 在 Chromium 项目中研发 Blink 渲染引擎（即浏览器核心），内置于 Chrome 浏览器之中。Blink 其实是 WebKit 的分支。大部分国产浏览器最新版都采用Blink内核。二次开发 |
| Opera   |     blink      | 现在跟随chrome用blink内核。                                  |

#### **1.2 web标准**

由w3c（万维网联盟）

**「构成」**👉 **结构，表现和行为**

- 结构标准用于对网页元素进行整理和分类(HTML)
- 表现标准用于设置网页元素的版式、颜色、大小等外观属性(CSS)
- 行为标准用于对网页模型的定义及交互的编写(JavaScript)

**「Web标准的优点」**👇

- 易于维护：只需更改CSS文件，就可以改变整站的样式
- 页面响应快：HTML文档体积变小，响应时间短
- 可访问性：语义化的HTML（结构和表现相分离的HTML）编写的网页文件，更容易被屏幕阅读器识别
- 设备兼容性：不同的样式表可以让网页在不同的设备上呈现不同的样式
- 搜索引擎：语义化的HTML能更容易被搜索引擎解析，提升排名

### 二 HTML基本结构

#### 2.1 基本结构标签

![image-20220127145434366](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220127145434366.png)

1. HTML 标签是由尖括号包围的关键词，例如 `<html>`
2. HTML 标签通常是成对出现的，例如 `<html>`和`</html>` ，我们称为双标签。标签对中的第一个标签是开始标签，第二个标签是结束标签。
3. 有些特殊的标签必须是单个标签（极少情况），例如`<br />`，我们称为单标签。

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
~~~

#### 2.2 文档类型声明标签

- `<!DOCTYPE>`文档类型声明，作用就是告诉浏览器使用哪种**HTML版本**来显示网页。

```html
<!DOCTYPE html>
```

- 这句代码的意思是: 当前页面采取的是 HTML5 版本来显示网页.
- 注意：
  - `<!DOCTYPE>` 声明位于文档中的最前面的位置，处于 `<html>` 标签之前。
  - `<!DOCTYPE>` 不是一个 HTML 标签，它就是文档类型声明标签。

#### 2.3 lang标签

用来定义当前文档显示的语言，简单来说就是定义成en也可以显示中文，定义成zh-CN也可以显示成英文。

- en 定义语言为英语
- zh-CN 定义语言为中文

```
<html lang="en">
```

#### 2.4 字符集

在`<head>`标签内，可以通过`<meta>` 标签的 charset 属性来规定 HTML 文档应该使用哪种字符编码。

```html
<meta charset="utf8">
```

- charset 常用的值有：：GB2312 、BIG5 、GBK 和 UTF-8，其中 UTF-8 也被称为万国码，基本包含了全世界所有国家需要用到的字符

### 三 HTML标签

#### 3.1 标题标签

```html
<body>
    <h1> 一级标题</h1>
    <h2> 二级标题</h2>
    <h3> 三级标题</h3>
    <h4> 四级标题</h4>
    <h5> 五级标题</h5>
    <h6> 六级标题</h6>
</body>
```

- 加了标题的文字会变的加粗，字号也会依次变大
- 根据重要性递减
- 一个标题独占一行

#### 3.2 段落标签

~~~html
<p>段落标签</p>
~~~

- paragraph 的缩写
- 文本在一个段落这种会根据浏览器窗口的大小进行自动换行
- 段落和段落之间保有空隙

#### 3.3 换行标签🔥

```html
<br />
```

- `<br />` 是个单标签
- `<br />` 标签只是简单的开始新的一行，中间没有垂直距离，跟段落不一样，段落之间会插入一些垂直的间距

#### 3.4 文本格式化标签

- 为文字设置**粗体、斜体、下划线**等效果

| 语义   | 标签                       |
| ------ | -------------------------- |
| 加粗   | `<strong></strong><b></b>` |
| 倾斜   | `<em><em>和<i></i>`        |
| 删除线 | `<del></del>和<s></s>`     |
| 下划线 | `<ins></ins>和<u></u>`     |

- 重点记忆 加粗 和 倾斜
- 推荐前面的，语义更强烈

#### 3.4 <div>和<span> 标签

两者都没有语义，就是一个盒子，来装内容的

- `<div></div>` :一行只能放一个大盒子，独占一行
- `<span></span>` : 一行可以放多个span，小盒子

#### 3.5 图像标签和路径

```html
<img src="图像url" alt="" title="" width="500" border="15"/>
```

- `src`是`<img>`标签的必须属性，它用于指定图像文件的路径和文件

| 属性   | 属性值   | 说明                                     |
| ------ | -------- | ---------------------------------------- |
| src    | 图片路径 | 必须属性                                 |
| alt    | 替换文本 | 替换文本（当图片不能显示时候显示的文字） |
| title  | 提示文本 | 提示文本（鼠标放到图像上，显示的文字）   |
| width  | 宽度     | 设置图片的宽度                           |
| height | 高度     | 设置图片的高度                           |
| border | 边框     | （一般不通过html设置，而是通过css设置）  |

#### 3.6 路径问题

##### 3.6.1 相对路径

| 相对路径分类 | 符号 | 说明                                                       |
| ------------ | ---- | ---------------------------------------------------------- |
| 同一级路径   |      | 图形文件位于 HTML 文件同一级 如`<img src="1.png">`         |
| 下一级路径   | /    | 图形文件位于 HTML 文件下一级 如 `<img src="images/1.png">` |
| 上一级路径   | …/   | 图形文件位于 HTML 文件上一级 如 `<img src="../1.png">`     |

##### 3.6.2 绝对路径

- 绝对路径：是指目录下的绝对位置，直接到达目标位置，通常是从盘符开始的路径或者完整的网络地址。

#### 3.7 超链接标签（！）

<a>标签用于定义超链接，作用是从一个页面连接到另一个页面。

**语法**

```
<a href="跳转目标" target="目标窗口的弹出方式">文本或图像</a>
```

| 属性   | 作用                                                         |
| ------ | ------------------------------------------------------------ |
| href   | 用于指定链接目标的url地址。必须属性                          |
| target | 用于指定连接页面的打开方式。`_self`为默认值当前窗口打开，`_blank`为在新窗口中打开 |

**链接分类**

1. 外部链接：`<a href="http://www.qq.com" target="_blank">腾讯</a>`

   - 地址一定是以http://开头

2. 内部链接：`<a href="index.html">主页</a>`

3. 空链接：如果没有确定链接目标时，`<a href='#'></a>`

4. 下载链接：如果href里面地址是一个文件或者压缩包，会下载这个文件

5. 网页元素链接：

   ```html
   <a href="http://www.baidu.com"> <img src=""> </a>
   <!--点击图片就自动找到百度页面了--!>
   ```

6. 锚点链接：点击链接，可以快速定位到页面中的某个位置

- 在链接文本的`href`属性中，设置属性值为 **#名字**
- 找到目标位置标签，里面添加一个 **id属性=刚才的名字**

#### 3.8 特殊字符

![在这里插入图片描述](https://img-blog.csdnimg.cn/d387d9bdf9ba47acbc0a9173fc7bfb5d.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

重点记住：空格、大于号、小于号 这三个，其余的使用的很少，如果需要使用回头查阅即可

#### 3.9 表格标签

- 表格用于显示、展示数据

- `table` 用来定义表格的标签
- `tr` 用来定义表格中的行，必须嵌套在`<table></table>` 标签中
- `td` 用来定义表格中的单元格，必须嵌套在`<tr></tr>` 标签中
- `th` 用来定义表格中的表头，表头单元格里面的内容**加粗居中**显示

- 表格属性一般都时用css设置

  ```html
   <table>
              <tr> <th>姓名</th>  <th>性别</th> <th>年龄</th></tr>
              <tr> <td>姓名</td>  <td>性别</td> <td>年龄</td></tr>
   </table>
  ```

  ###### **表格属性**

  表格标签的属性实际开发并不常用，因为基本都是通过后面的CSS来设置的

  | 属性名      | 属性值            | 描述                                              |
  | ----------- | ----------------- | ------------------------------------------------- |
  | align       | left,center,right | 规定表格相对周围元素的对齐方式                    |
  | border      | 1或者’’ ‘’        | 规定表格单元是否拥有边框，默认为" "，表示没有边框 |
  | cellpadding | 像素值            | 规定单元边沿与其内容之间的空白，默认1像素         |
  | cellspacing | 像素值            | 规定单元格之间的空白，默认2像素                   |
  | width       | 像素值或百分比    | 规定表格的宽度                                    |

###### 	**表格结构标签**	

​	为了更好的表示表格的语义，可以将表格分割成 表格头部 和表格主体两大部分

- 用 `<thead></thead>` 标签表示表格的头部区域，`<thead>`内部必须拥有`<tr>`标签，一般是位于第一行
- 用`<tbody></tbody>` 标签表示表格的主体区域，主要是用于放数据本体
- 以上标签都是放在`<table></table>`标签中

![在这里插入图片描述](https://img-blog.csdnimg.cn/b20e2df070ce41b8ba0d5ea101efd153.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

###### 合并单元格

- 跨行合并：`rowspan=“合并单元格的个数”`

- 跨列合并：`colspan="合并单元格的个数"`

  <img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220127170340782.png" alt="image-20220127170340782" style="zoom:50%;" />

- **目标单元格**（写合并代码）

  - 跨行：最上侧单元格为目标单元格，写合并代码
  - 跨列：最左侧单元格为目标的那远哥，写合并代码

- **合并单元格三部曲**

  - 先确定跨行还是跨列
  - 找到目标单元格，写上合并方式=合并单元格的数量，比如<td colspan="2"></td>
  - 删去多余单元格

```html
 <table border="1" width="500">
            <tr> <th>姓名</th>  <th>性别</th> <th>年龄</th></tr>
            <tr> <td>姓名</td>  <td>性别</td> <td>年龄</td></tr>
            <tr> <td>姓名</td>  <td>性别</td> <td>年龄</td></tr>
            <tr> <td>姓名</td>  <td>性别</td> <td>年龄</td></tr>
</table>
修改为
 <table border="1" width="500">
            <tr> <th>姓名</th>  <th>性别</th> <th>年龄</th></tr>
            <tr> <td>姓名</td>  <td colspan="2">性别</td> </tr>
            <tr> <td>姓名</td>  <td>性别</td> <td>年龄</td></tr>
            <tr>  <td>性别</td> <td>年龄</td></tr>
</table>
```

![image-20220127171307463](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220127171307463.png)

- 标签：table标签 => tr行标签 => td 单元格 => th 表头单元格 => thead表格头部区域标签 =》 tbody 表格主题区域标签
- 属性：align border width....
- 合并单元格

#### 3.10 列表标签

- 用于布局
- 无序列表：`<ul>`
- 有序列表：`<ol>`
- 自定义列表：`<dl>`

| 标签名      | 定义       | 说明                                             |
| ----------- | ---------- | ------------------------------------------------ |
| `<ul></ul>` | 无序列表   | 里面只能嵌套li！没有顺序。li里面可以包含任何标签 |
| `<ol></ol>` | 有序列表   | 里面只能包含li！有顺序                           |
| `<dl></dl>` | 自定义列表 | 里面只能包含dt和dd，dt和dd里面可以放任何标签     |

###### 无序列表

~~~html
 <ul>
        <li>奶茶</li>
        <li>火锅</li>
        <li>串串</li>
</ul>
~~~

- ul里面只能放li，li里面放什么都可以
- 无序列表的各个列表项之间没有顺序之分，是并列的
- 用css设置样式

###### 有序列表

```html
<ol>
    <li>列表1</li>
    <li>列表2</li>
    <li>列表3</li>
</ol>
```

- 有序列表的各个列表项之间有顺序之分。
- ol里面只能放li，li里面放什么都可以
- 用css设置样式

###### 自定义列表

![image-20220127173415444](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220127173415444.png)

~~~html
<dl>
     <dt>关注我们</dt><!--上面有个小标题!-->
     <dd>新浪微博</dd>
     <dd>联系我们</dd>
</dl>
~~~

- <dl></dl>中只能包含dt和dd

- 经常是一个dt对应多个dd

- dt和dd属于兄弟关系

#### 3.11 表单标签

- 表单用于**收集用户信息**，例如注册页面等等
- 一个完整的表单通常由**表单域，表单控件（表单元素）和提示信息**3部分组成

![在这里插入图片描述](https://img-blog.csdnimg.cn/ccddea3e9d4b42b0b4ac8713741bde00.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

###### 表单域

- 表单域是一个包含表单元素的区域

- `<form></from>`标签用于定义表单域，**实现用户信息的收集**，会把它范围内的表单元素信息提交给服务器

```html
<form action="url地址" method="提交方式" name="表单域的名称">
    
</form>
```

| 属性   | 属性值   | 作用                                               |
| ------ | -------- | -------------------------------------------------- |
| action | url地址  | 用于指定接收并处理表单数据的服务器程序的url地址    |
| method | get/post | 用于设置表单数据的提交方式，其取值为get或post      |
| name   | 名称     | 用于指定表单的名称，以区分同一个页面中的多个表单域 |

###### 表单控件（元素）

**①input输入表单元素**

- `input`输入表单元素
- `input`是个单标签，`type` 属性设置不同的属性用来指定不同的控件类型(文本字段、复选框、单选按钮、按钮等)

```html
     <form action="xxx.php" method="GET" name="name1">
    用户名<input type="text" name="username" value="请输入用户名" maxlength="6"> <br>
    密码<input type="password" name="password" value="password"> <br>
    <!-- name是表单元素名字 这里性别单选按钮必须有相同的名字name 才可以实现多选1 -->
    <!-- 单选按钮和复选框可以设置初始选中的按钮 -->
    性别 男<input type="radio" name="sex" value="男"> 女<input type="radio" name="sex" value="女" checked="checked"><br>
    爱好 体育<input type="checkbox" name="hobby" value="吃饭" checked="checked"> 吃饭<input type="checkbox" name="hobby" value="睡觉"><br>
    <input type="submit" value="免费注册">
    <!-- 点击提交按钮把，把表单域form里面的值提交给后台 -->
    <input type="reset" value="重新设置">
    <!-- 重置按钮可以重置表单元素的初始默认状态 -->
    <input type="button" value="获取短信验证码">
    <!-- 后期搭配js使用 -->
    上传头像<input type="file">
    <!-- 文件域 上传文件用的 -->
   </form>
```

type 属性的属性值及描述如下：

| 属性值   | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| button   | 可点击按钮(多数情况下，用于通过JavaScript启动脚本)           |
| checkbox | 复选框                                                       |
| file     | 输入字段和"浏览"按钮，供文件上传。                           |
| hidden   | 隐藏的输入字段                                               |
| image    | 图像形式的提交按钮                                           |
| password | 密码框。定义密码字段。该字段中的字符被掩码                   |
| text     | 文本框。定义单行的输入字段，用户可在其中输入文本。默认宽度为 20 个字符。 |
| radio    | 单选按钮。多选一                                             |
| reset    | 重置按钮。重置按钮会清楚表单中的所有数据。                   |
| submit   | 提交按钮。提交按钮会把表单数据发送到服务器。                 |

除 type 属性外，`<input>` 标签还有很多其他很多属性，其常用属性如下：

| 属性      | 属性值       | 描述                                                    |
| --------- | ------------ | ------------------------------------------------------- |
| name      | 由用户自定义 | 定义 input 元素的名称，不显示在页面上                   |
| value     | 由用户自定义 | 规定 input 元素的值，显示在页面上，可以把数据传输到后台 |
| checked   | checked      | 规定此 input 元素首次加载时应当被选中                   |
| maxlength | 正整数       | 规定输入字段中字符的最大长度                            |

- name 和 value 是每个表单元素都有的属性值，主要给后端人员使用。

- name 是表单元素的名字，要求 单选框和复选框要有相同的name值

- checked 属性主要针对于单选框和复选框，主要作用是一打开页面，就可以默认选中某个表单元素
- maxlength较少用，限制用户输入字符数。

**问题：**

1.  有些表单元素想要打开的时候就有初始值，需要怎么设置？

   可以给表单元素设置value 属性="值"

   ```html
   <input type="text" value="请输入用户名"/>
   ```

2. 页面中表单元素很多，如何区分不同的表单元素？

   - name
   - 单选框和复选框如果是同一组，需要给他们设置一样的名字。

   ```html
   <input type="text" name="username"/>
   ```

3. 页面一打开就让某个单选框或者复选框是选中状态？

   checked属性

   ```html
   <input type="radio" name="sex" value="男" checked="checked"/>
   ```

4. 如何让input表单元素展示出不同的形态？比如单选按钮或者文本框

   type属性

**label标签（一般和input搭配起来使用）**

- `label`标签用于绑定一个表单元素，当点击`<lable>`标签内的文本时，浏览器就会自动将焦点(光标)转到表单元素上，用来增加用户体验

- `label`标签的 for属性 = 相关元素的id 属性

  ```html
  <label for="sex"> 男 </lable>
  <input type="radio" name="sex" id="sex" />
  ```

**②select下拉表单元素**

- 下拉表单元素

- `<select>`中至少包含一对`<option>`

- 在`<option>`中定义 `selected="selected"` 时，当前项即为默认选中项

  ```html
   <form>
          籍贯<select>
              <option >山东</option>
              <option selected="selected">北京</option>
              <option>安徽</option>
              <option>陕西</option>
          </select>
     </form>
  ```

**③textarea文本域元素**

- 用于定义多行文本输入的控件(留言，用户输入较多的情况)

~~~HTML
<form>
    今日反馈：
    <textarea cols="50" rows="5">lalal </textarea>
</form>
~~~

###### 查阅文档

W3C: [w3school 在线教程](https://www.w3school.com.cn/)

MDN:[MDN Web Docs (mozilla.org)](https://developer.mozilla.org/zh-CN/)

