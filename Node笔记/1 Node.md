##  1 为什么要学习Node.js

- 企业需求
- 具有服务端开发经验更改
- front-end
- back-end
- 全栈开发工程师
- 基本的网站开发能力
- 服务端
- 前端
- 运维部署
- 多人社区

###  1.1 Node.js是什么

- Node.js是JavaScript 运行时
- 通俗易懂的讲，Node.js是JavaScript的运行平台
- Node.js既不是语言，也不是框架，它是一个平台
- 浏览器中的JavaScript
  - EcmaScript
    - 基本语法
    - if
    - var
    - function
    - Object
    - Array
- Bom
- Dom
- Node.js中的JavaScript
  - 没有Bom，Dom
  - EcmaScript
  - 在Node中这个JavaScript执行环境为JavaScript提供了一些服务器级别的API
    - 例如文件的读写
    - 网络服务的构建
    - 网络通信
    - http服务器
- 构建于Chrome的V8引擎之上
  - 代码只是具有特定格式的字符串
  - 引擎可以认识它，帮你解析和执行
  - Google Chrome的V8引擎是目前公认的解析执行JavaScript代码最快的
  - Node.js的作者把Google Chrome中的V8引擎移植出来，开发了一个独立的JavaScript运行时环境
- Node.js uses an envent-driven,non-blocking I/O mode that makes it lightweight and efficent.
  - event-driven 事件驱动
  - non-blocking I/O mode 非阻塞I/O模型（异步）
  - lightweight and efficent. 轻量和高效
- Node.js package ecosystem,npm,is the larget scosystem of open source libraries in the world
  - npm 是世界上最大的开源生态系统
  - 绝大多数JavaScript相关的包都存放在npm上，这样做的目的是为了让开发人员更方便的去下载使用
  - npm install jquery

###  1.2 Node能做什么

- web服务器后台
- 命令行工具
  - npm(node)
  - git(c语言)
  - hexo（node）
  - ...
- 对于前端工程师来讲，接触最多的是它的命令行工具
  - 自己写的很少，主要是用别人第三方的
  - webpack
  - gulp
  - npm

## 2 起步

### 2.1 安装Node环境

- 查看Node环境的版本号
- 下载：https://nodejs.org/en/
- 安装：
  - 傻瓜式安装，一路`next`
  - 安装过再次安装会升级
- 确认Node环境是否安装成功
  - 查看node的版本号：`node --version`
  - 或者`node -v`
- 配置环境变量

### 2.2 解析执行JavaScript

1. 创建编写JavaScript脚本文件
2. 打开终端，定位脚本文件的所属目录
3. 输入`node 文件名`执行对应的文件

注意：文件名不要用`node.js`来命名，也就是说除了`node`这个名字随便起，最好不要使用中文。

###  2.3 文件的读写

#### 文件读取

```javascript
//浏览器中的JavaScript是没有文件操作能力的
//但是Node中的JavaScript具有文件操作能力
//fs是file-system的简写，就是文件系统的意思
//在Node中如果想要进行文件的操作就必须引用fs这个核心模块
//在fs这个核心模块中，就提供了所有文件操作相关的API
//例如 fs.readFile就是用来读取文件的

//  1.使用fs核心模块
var fs = require('fs');

// 2.读取文件
fs.readFile('./data/a.txt',function(err,data){
   if(err){
        console.log('文件读取失败');
   }
    else{
         console.log(data.toString());
    }
})
```

#### 文件写入

```javascript
//  1.使用fs核心模块
var fs = require('fs');

// 2.将数据写入文件
fs.writeFile('./data/a.txt','我是文件写入的信息',function(err,data){
   if(err){
        console.log('文件写入失败');
   }
    else{
         console.log(data.toString());
    }
})
```

## 3 Node中的JavaScript

- EcmaScript  
  - 基本的JS语法，没有DOM BOM
- 核心模块  服务器级别的API ： 文件操作能力  http服务能力
- 第三方模块
- 用户自定义模块

### 3.1EcmaScript  

### 3.2核心模块

Node为JS提供了**很多服务器级别的API**，这些API绝大多数都被包装到了一个具名的核心模块中了。

例如文件操作的`fs`核心模块，http服务构建的`http`模块，`path`路径操作模块，`os`操作系统模块。。。

以后只要说这个模块是一个核心模块，就要马上想到如果要使用他，就必须

```javascript
var fs = require('fs')
var http = require('http')
require('./b.js')   //可以通过require在一个文件中执行另一个文件
				//在node中，没有全局作用域，只有模块作用域（简单来讲就是文件作用域）
```

最简单的http服务：

```javascript
//接下来，要使用node 构建一个web服务器
//在node 中专门提供了一个核心模块：http
//http这个模块的职责是帮你创建编写服务器

//1.加载http核心模块
var http = require('http')

//2.使用http.createServer() 方法创建一个Web服务器
// 返回一个Server实例

var server = http.createServer()

//3.服务器要干嘛？
//  提供服务： 对数据的服务
//  发请求
//  接受请求
//  处理请求
//  给个反馈（发送响应）
//  当客户端请求过来，就自动触发服务器的request请求时间，然后执行第二个参数：回调函数
server.on('request',function(){
console.log('收到请求')
})

//4.绑定端口号,启动服务器
server.listen(4000,function(){
    console.log('服务器启动成功')
})
```

![image-20211024162034466](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20211024162034466.png)



- 浏览器默认以80为端口号

- favicon.ico网站图标，浏览器的默认行为

- Apache就是个软件，提供Web服务的

- IP地址用来定位计算机

- 端口号用来定位具体的应用程序

- （所有需要联网通信的软件都必须有端口号）

  <img src="D:\学习\字节创新班\nodejs资料（7天）\01\ip地址和端口号.png" style="zoom:150%;" />

### 3.3 用户自定义模块

- require
- exports

**模块系统：**

- 在node中没有全局作用域的概念
- 在node中，只能通过require方法来加载多个JavaScript脚本文件
- require加载只能是执行其中的代码，文件与文件之间由于是模块作用域，所以不会有污染的
  - 模块完全是封闭的
  - 外部无法访问内部
  - 内部也无法访问外部

- 模块作用域固然带来了一些好处，可以加载执行多个文件，可以完全避免变量命名冲突
- 但是某些情况下，模块与模块之间是需要通信的
- 在每个模块中都提供了一个对象：`exports`
- 该对象默认是一个空对象
- **你要做的就是把需要被外部访问使用的成员手动的挂载到`exports`接口对象中**
- **然后谁来`require`这个模块，谁就可以得到模块内部的`exports`接口对象**
- 还有其他的一些规则，具体后面讲，以及如何在项目中使用这种编程方式，会通过后面的案例讲解

**核心模块：**

- 核心模块是由Node提供的一个个的具名的模块，它们都有自己特殊的名称标识，例如

  - fs文件操作模块
  - http网络服务构建模块
  - os操作系统信息模块
  - path路径处理模块
  - 。。。

- 所有核心模块在使用的时候都必须手动的先使用`require`方法来加载，然后才可以使用。例如

  `var fs = require('fs')`



## 4 Web 服务器开发

#### 4.1 Ip地址和端口号

- ip地址用来定位计算机
- 端口号用来定位具体的应用程序
- 一切需要联网通信的软件都会占用一个端口号
- 端口号范围0-65536之间
- 在计算机中有一些默认端口号，最好不要去舒勇
  - 例如http服务的80

- 我们在开发过程中使用一些简单好记的就可以了，例如3000、5000等没什么含义
- 可以同时开启多个服务，但一定要确保不同服务占用的端口号不一致
- 在一台计算机中，同一个端口号同一时间只能被一个程序占用

#### 4.2 Content-Type

- 用于定义网络文件的类型和网页的编码，决定浏览器将以什么形式、什么编码读取这个文件.

- 服务器最好把每次响应的数据是什么内容类型都告诉客户端，而且要正确的告诉
- 不同的资源对应的Content-Type是不一样的，一般只为字符数据才指定编码，具体参照 http://tool.oschina.net/commons
- 图片不需要指定编码

#### 4.3通过网络发送文件

- 发送的并不是文件，本质发送的是文件的内容
- 当浏览器收到服务器响应内容之后，就会根据`Conten-Type`进行对应的解析处理



## 6 Node 中的模块系统

- 使用Node编写应用程序主要就是在使用：

- EcmaScript语言

  - 和浏览器不一样，在Node中没有DOM,DOM

- 核心模块

  - 文件操作的fs

  - http服务的http
  - url路径操作模块
  - path路径模块
  - os操作系统信息

- 第三方模块

  - art-template
  - 必须通过npm下载使用

- 自己写的模块

  - 自己创建的文件

### 6.1 什么是模块化

- 文件作用域

- 通信规则

  - 加载  require

  - 导出

### 6.2 commomJS模块规范

在Node中的JS有一个很重要的概念：模块系统。

- 模块作用域
- 使用require方法加载模块
- 使用exports接口对象来导出模块中的成员

#### 6.2.1 加载require

语法：

```
var 自定义变量名称 = require('模块')
```

两个作用：

- 执行被加载模块中的代码
- 得到被加载模块中的`exports`导出接口对象

#### 6.2.2 导出`exports`

Node 中是模块作用域，默认文件中所有的成员旨在当前文件模块有效

对于希望可以被其他模块访问的成员，我们就需要把这些公开的成员都挂载到`exports`接口对象中就可以了

导出多个成员（必须在对象中）：

```javascript
exports.a = 123
exports.b = 'hello'
exports.c = function(){
	console.log('ccc')
}
exports.d = {
    foo:'bar'
}

```

导出单个成员（拿到的就是：函数，字符串）：

```javascript
 module.exports = 'hello'
```

以下情况会覆盖：

```javascript
module.exports = 'hello'
//以这个为准，后者会覆盖前者
module.exports = function(x,y){
    return x + y
}
```

导出多个成员：

```
exports.a = add
```

也可以这样导出多个成员

```javascript
module.exports = {
    add:function(){
        
    },
    str:'hello'
}
```

####	6.2.3 原理解析

`exports`是`module.exports`的一个引用

```javascript
console.log(exports === module.exports)//true

exports.foo = 'bar'
//等价于

module.exports.foo = 'bar'
```

- 真正去使用的时候：
- 导出多个成员：exports.xxx = xxx
- 导出单个成员：module.exports

#### 6.2.5 require方法加载规则

深入浅出Nodejs  模块机制  书

[(15条消息) 【深入浅出Node.js系列三】深入Node.js的模块机制_zhangyuan19880606的专栏-CSDN博客](https://blog.csdn.net/zhangyuan19880606/article/details/51508699)

- 核心模块
  - 模块名

- 用户自己写的
  - 路径形式文件模块

- 优先从缓存加载

- 第三方模块

  - 模块名

- 判断模块标识
  - 核心模块：本质也是文件，已经被编译到了二进制文件中，只需要按照名字加载就可以

  - 第三方模块：凡是第三方模块必须通过npm加载，使用的时候可以通过`require`（‘包名’）的方式来进行加载才可以使用

    `var template = require('art-template')`

    不可能有任何一个第三方包和核心模块的名字是一样的

    既不是核心模块也不是路径形式的模块：

    - 先找到当前文件所处目录中的`node_modules`目录

    - 找`node_modules/art-template`

    - 再找`node_modules/art-template/package.json`文件中的main属性
    - main属性中就记录了`art-template`的入口模块，然后加载使用这个第三方包
    - 实际上最终加载的还是文件
    - 如果`package.json`文件不存在或者`main`指定的入口模块也没有
    - 则`node`会自动找该目录下的`index.js`，`index.js`作为一个默认备选项
    - 如果以上所有任何一条都不成立，则会进入上一级目录中的`node_modules`。。。直到当前磁盘根目录都找不到，报错`can not find module`
    - `node_modules`只有一个，放在项目根目录

  - 自己写的模块

### 6.3 npm

- node package manager

####	6.3.1 npm网站

> ​	www.npmjs.com npm官方网站

#### 6.3.2 npm命令行工具

npm的第二层含义就是一个命令行工具，只要你安装了node就已经安装了npm，npm也有版本这个概念，可以通过在命令行输入

```javascript
npm --version
```

升级npm:

```JavaScript
npm install --global npm
```

#### 6.3.3 npm常用命令

- npm init
  - npm init -y 可以跳过向导，快速生成
- npm install
  - 一次性把dependencies选项中的依赖项全部安装
  - npm i
- npm install 包名：
  - 只下载
  - npm i 包名
- npm install --save 包名
  - 下载并且保存依赖项（package.json文件中的dependencies选项）
  - npm i-S 包名
- npm uninstall 包名
  - 只删除，如果有依赖项会保存
  - npm un 包名
- npm uninstall --save 包名
  - 删除的同时也会把依赖信息去除
  - npm un-S 包名
- npm --help
  - 查看使用帮助
- npm 命令 --help
  - 查看指定命令使用帮助
  - 例如`npm uninstall --help`

#### 6.3.4 解决npm被墙问题

npm存储包文件的服务器在国外，有时候会被墙，速度很慢，所以需要解决这个问题

http://npm/taobao.org/ 淘宝的开发团队把npm在国内做了备份

安装淘宝的cnpm：

```shell
#在任意目录执行都可以
#--global表示安装在全局，而非当前目录
#--global不能省略，否则不管用
npm install --global cnpm
```

接下来你安装包的时候把之前的npm替换成cnpm

例如：

```shell
#使用cnpm就会通过淘宝的服务器来下载jquery
cnpm install jquery
```

如果不想安装cnpm又想使用逃吧的服务器来下载

```shell
npm install jquery --registry=http://registry.npm.taobao.org
```

但是每一次手动添加参数很麻烦，所以可以把这个选项按加入配置文件中：

```shell
npm config set registry http://registry.npm.taobao.org

#查看npm配置信息
npm config list
```

只要经过了上面命令的配置，则以后所有npm install都会默认通过淘宝的服务器来下载

### 6.4 package.json

建议每一个项目都要有一个package.json 文件（包描述文件，就像产品说明书一样），给人踏实的感觉

这个文件可以通过`npm init`的方式自动初始化出来

![image-20211026233204106](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20211026233204106.png)

![image-20211026233223815](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20211026233223815.png)

![image-20211026233025940](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20211026233025940.png)

![](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20211026233135905.png)

目前来讲，最有用的是`dependencies`选项，可以用来帮我们保存第三方包信息

- 建议每个项目的根目录下都有一个`package.json`文件

- 建议执行`npm insall` 包名的时候都加上`--save`这个选项，目的是用来保存依赖项信息

- 如果`node_modules`删除了也不用担心，只需：`npm install` 就会把`package.json`中的`dependencies`依赖项都下载回来


### 6.5 path路径操作模块

- path.basename
  - 获取路径的文件名（默认包含扩展名）
- path.dirname
  - 
- path.extname
  - 获取一个路径中的扩展名部分
- path.parse
  - 把一个路径转为对象
    - root根目录
    - dir目录
    - base包含后缀名的文件名
    - ext后缀名
    - name不包含后缀名的文件名
- path.join
  - 当你需要进行路径拼接的时候，推荐使用这个方法
- path.isAbsolute
  - 判断一个路径是否是绝对路径

### 6.6 Node中的其他成员

在每个模块中，除了`require`,`exports`等模块相关API外，还有两个特殊的成员：

- `__dirname`**动态获取**可以用来获取当前文件模块所属目录的绝对路径
- `__filename`**动态获取**可以用来获取当前文件的绝对路径
- `__dirname` 和 `__filename` 不受执行node命令所属路径影响的

在文件操作中，使用相对路径是不可靠的，因为在Node中文件操作的路径被设计为相对于执行node命令所处的路径（不是bug，人家这样设计是有使用场景的）

这里我们就可以使用`__dirname`或者`__filename`来解决问题

为了尽量避免问题，以后再文件操作中使用的相对路径都统一转换位 **动态的绝对路径**



## 7 Express

原生的http在某些方面表现不足以应对我们的开发需求，所以我们就需要使用框架来加快我们的开发效率，让我们的代码更高度统一

在Node 中，有很多Web开发框架，我们这里学习Express为主

> ​	http://expressjs.com/

![image-20211027121757303](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20211027121757303.png)

### 7.1起步

安装：

```shell
npm install express
```

#### 7.1.2 hello world

```javascript
var express= require('express')

var app = express()

app.get('/',function(req,res){
      res.send('Hello world')
})

app.listen(3000,function(){
  console.log('express app is running')
})
```

#### 7.1.3 基本路由

路由器：router，连接多个用户，路由就是一张表，这个表里面有具体的映射关系

**get：**

```JavaScript
//当你以GET方法请求/的时候，执行对应的处理函数
app.get('/',function(req,res){
      res.send('Ho world')
})
```

**post：**

```JavaScript
//当你以post方法请求/的时候，执行对应的处理函数
app.post('/',function(req,res){
      res.send('Ho world')
})
```

####	7.1.4 静态服务

> ​	[利用 Express 托管静态文件 - Express 中文文档 | Express 中文网 (expressjs.com.cn)](https://www.expressjs.com.cn/starter/static-files.html)

```javascript
//当以/public/开头的时候，去./public/目录中找对应的资源
app.use('/public/',express.static('./public/'))

app.use(express.static('./public/'))
```

### 7.2 在Express中配置使用Art-template模板引擎

[art-template - Github 仓库](https://github.com/aui/art-template)

[art-template - 官方文档](http://aui.github.io/art-template/zh-cn/index.html)

安装：

~~~shell
npm install --save art-template
npm install --save express-art-template
~~~

配置：

~~~js
app.engine('html', require('express-art-template'));
~~~

使用：

```js
//默认会去项目中的views目录去找index.html
app.get('/', function (req, res) {
    res.render('index.html', {
        user: {
            name: 'aui',
            tags: ['art', 'template', 'nodejs']
        }
    });
});
```

如果希望修改默认的`views`试图渲染存储目录，可以：

```js
//第一个参数views不能写错！！
app.set('views',目录路径)
```

### 7.3  解析表单get请求体（在express获取表单Get请求数据）

express内置了一个API，可以通过req.query获取

```js
req.query
```



### 7.4 解析表单post请求体（在express获取表单Post请求数据）

在Express中没有内置获取表单POST请求体的API，这里我们需要使用一个第三方包：`body-parser`

安装：

```
npm install --save body-parser
```

配置：

```js
var  express = require('express')
// 引包
var bodyParser = require('body-parser')

var app = express()

//配置body-parser
//只要加入这个配置，则在req请求对象上会多出来一个属性：body
//也就是你可以直接通过req-body来获取表单POST请求体数据了
// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }))
// parse application/json
app.use(bodyParser.json())

```

使用：

```js
app.use(function (req, res) {
  res.setHeader('Content-Type', 'text/plain')
  res.write('you posted:\n')
  //可以通过req.body来获得表单数据
  res.end(JSON.stringify(req.body, null, 2))
})
```

### 7.5 CRUD案例

#### 模块化思想

模块如何划分：

- 模块职责单一

#### 起步

- 初始化
- 安装依赖
- 模板处理

#### 路由设计

| 请求方法 |     请求路径     | get参数 |          post参数          |        备注        |
| :------: | :--------------: | :-----: | :------------------------: | :----------------: |
|   GET    |    /students     |         |                            |      渲染首页      |
|   GET    |  /students/new   |         |                            |   渲染学生添加页   |
|   POST   |  /students/new   |         |  name,age,gender,hobbies   | 处理并添加学生请求 |
|   GET    |  /students/edit  |   id    |                            |    渲染编辑页面    |
|   POST   |  /students/edit  |         | id,name,age,gender,hobbies |    处理编辑请求    |
|  DELETE  | /students/delete |   id    |                            |    处理删除请求    |

#### 提取路由模块

router.js

```js
/**
 * router.js 路由模块
 * 职责：
 *      处理路由
 *      根据不同的请求方法请求路径设置处理函数
 * 模块职责要单一
 * 我们划分模块的目的就是为了增强项目代码的可维护性
 */

//需要再这个文件中拿
var fs = require('fs')

//express提供了一种更好的方式
//专门用来包装路由
var express = require('express')

//1.创建一个路由容器
var router = express.Router()

//2.把路由容器都挂在到router路由容器中
router.get('/students',function(req,res){
    fs.readFile('db.json','utf-8',function(err,data){
        if(err){
            return res.status(500).send('Server Error')
        }

        var students = JSON.parse(data).students
        res.render('index.html',{
            "lists":[
                {
                name:'No1',
                text:'橘子'
            },
            {
                name:'No2',
                text:'橘子'
            },
            {
                name:'No3',
                text:'橘子'
            }
            ],
            students:students
        })
    })
})

router.get('/students/new',function(req,res){
 //render默认去views里面找
    res.render('new.html')
})

router.post('/students/new',function(req,res){
    //1.获取表单数据
    //2.处理
    //      将数据保存到db.json文件中用以持久化
    //3.发送响应
    //先读取出来，转成对象
    //然后往对象中push
    //把对象转为字符串
    //把字符串再一次写入文件
    console.log(req.body)
    fs.readFile('db.json',function(err,data){
        if(err)
        res.send('404 Not found')
        else{
            var data = data.toString()

            console.log(data)
            //res.render('index.html',data)
            res.redirect('/students')
        }
    })

})

router.get('/students/edit',function(req,res){
   
})

router.post('/students/edit',function(req,res){
    
})

router.get(' /students/delete',function(req,res){
    
})

//3.把router导出
module.exports = router
```

app.js:

```js
var router = require('./router')

//挂载路由
app.use(router)
```

#### 设计操作数据的API文件模块

```js
/**
 * student.js
 * 数据操作文件模块
 * 职责：操作文件中的数据，只处理数据，不关心业务
 */

 var dbpath = './db.json'
/**
 * 获取所有学生列表
 * callback中的参数
 *  第一个参数是err
 *      成功是null
 *      错误是错误对象
 *  第二个参数是    结果
 *      成功是数组
 *      错误是undefined
 * return []
 */


var fs = require('fs')

exports.find = function(callback){
    //由于文本读出的data是二进制数据，需要转化为字符串：
    //可以设置二进制编码"utf-8"
    //也可以通过tostring()函数转字符串
    fs.readFile(dbpath,'UTF-8',function(err,data){
        if(err){
            return callback(err)
        }
        callback(null, JSON.parse(data).students)
    })
}

/**
 * 添加保存学生
 */
 exports.save = function(student,callback){
    fs.readFile(dbpath,'UTF-8',function(err,data){
        if(err){
            return callback(err)
        }
        var students = JSON.parse(data).students
        
        //处理id问题,不重复，记得减一！！！不然会报错找不到id是什么！！！
        if((students.length-1)>=0)
        student.id = students[students.length-1].id+1
        else student.id = 1
        //把用户传递的对象保存到数组中
        students.push(student)
        //把对象数据转化为字符串
        var file = JSON.stringify({
            students:students
        })
        fs.writeFile(dbpath,file,function(err){
            if (err)
            return callback(err)
            callback(null)
        })
    })
}

/**
 * 更新学生
 */
 exports.update = function(id,callback){
    fs.readFile('./db.json','UTF-8',function(err,data){
        if (err){
            callback(err)
        }
        var students = JSON.parse(data).students
        var student = students[id-1]
        // console.log(student)
        callback(null,student)
    })
}

exports.updatesave = function(student,callback){
    fs.readFile(dbpath,'UTF-8',function(err,data){
        if(err){
            return callback(err)
        }
        var students = JSON.parse(data).students

        //处理id问题,不重复，记得减一！！！不然会报错找不到id是什么！！！
        var num = student.id
        //把用户传递的对象保存到数组中
        console.log(student)
        students.splice(num-1,1,student) 
        // console.log(students)
        //数组id重新   
        students.forEach(function(value,index){
            value.id = index + 1
        })  
        //把对象数据转化为字符串
        var file = JSON.stringify({
            students:students
        })
        fs.writeFile(dbpath,file,function(err){
            if (err)
            return callback(err)
            callback(null,students)
        })
    })
}
/**
 * 删除学生
 */
 exports.delete = function(id,callback){
    fs.readFile('./db.json',function(err,data){
        if (err){
            callback(err)
        }
        var students = JSON.parse(data).students
        console.log(id)
        students.splice(id-1,1)
        students.forEach(function(value,index){
            value.id = index + 1
        })
        var file = JSON.stringify({
            students:students
        })
        fs.writeFile('./db.json',file,function(err){ 
            if(err){
                callback(err)
            }
            console.log(students)
            callback(null,students)
        })
    })
}
```



#### 自己编写的步骤

- 处理模板
- 配置开放静态资源
- 简单路由:/students渲染静态页出来
- 路由设计
- 提取路由模块
- 由于接下来一系列业务操作需要处理文件，所以我们需要封装student.js
  - 查询所有学生列表的API  find
  - findById
  - save
  - updateById
  - updateSave
  - deleteById

- 实现具体功能
  - 通过路由收到请求
  - 接受数据请求（get，post）
    - ​	req.query
    - ​    req.body
  - 调用数据操作API处理数据
  - 根据操作结果给客户端发送响应
- 业务功能顺序
  - 列表
  - 添加
  - 编辑
  - 删除

### 8 MongoDB

[NoSQL 简介 | 菜鸟教程 (runoob.com)](https://www.runoob.com/mongodb/nosql.html)

#### 8.1 关系型数据库和非关系型数据库

表就是关系

或者说表与表之间存在关系

- 所有的关系型数据库都需要通过sql语言来操作
- 所有的关系型数据库都要设计表结构
- 而且数据表还支持约束
  - 唯一的
  - 主键
  - 默认值
  - 非空

- 非关系型数据库非常灵活
- 有的非关系型数据库就是Key-value对
- MongoDB是长得最像关系型数据库的非关系型数据库
  - 数据库
  - 数据表
  - 表记录  文档对象
- MongoDB不需要设计表结构
- 也就是说你可以任意的往里面存数据，没有结构性这么一说

#### 8.2 安装MongoDB

- 下载：下载地址：[MongoDB Community Download | MongoDB](https://www.mongodb.com/try/download/community)

- 安装

- 配置环境

  将bin的地址添加到path中

- 最后输入 `mongod --version`测试是否安装成功

  ![image-20211103194934484](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20211103194934484.png)

#### 8.3 启动和关闭数据库

启动方式

```shell
# mongod 默认使用执行mongod 命令所处盘符根目录下的/data/db作为自己的数据存储目录
# 所以在第一次执行该命令之前自己先手动新建一个/data/db
```

如果想要修改默认的数据存储目录，可以：

```shell
mongod --dbpath=数据存储目录路径
```

停止

```shell
在开启服务的控制台，直接Ctrl+C 即可停止
或者直接关闭开启服务的控制台
```

#### 8.4 连接和退出数据库

连接：

```shell
# 该命令默认连接本机的MongoDB服务
mongo
```

退出：

```shell
#在连接状态输入exit退出连接
exit
```

#### 8.5 基本命令

- `show dbs`
  - 查看显示数据库
- `db`
  - 查看当前连接/操作的数据库

- `use数据库名称`
  - 切换到指定的数据（如果没有会新建）

- 插入数据

```shell
db.students.insertOne({"name":"JACK"})
```

####	8.6 在node中如何操作MongoDB数据

##### 8.6.1 使用官方的 `mongoDB`包来操作

> ​	[GitHub - mongodb/node-mongodb-native: The Official MongoDB Node.js Driver](https://github.com/mongodb/node-mongodb-native)

##### 8.6.2 使用第三方 mongoose 来操作MongoDB 数据库

第三方包： `mongoose`基于MongoDB官方的 `mongodb`包再一次做了封装

#### 8.7 使用Node操作MySQL数据库

### 10 异步编程

#### 10.1回调函数

#### 10.2 promise

> ​	参考文档阮一峰ecmascript

![image-20211124165531857](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20211124165531857.png)

- callback hell 无法保证顺序的代码
- 异步编程无法保证执行顺序

```js
//无法保证顺序的代码
var fs = require('fs')

fs.readFile ('./data/a.txt','utf-8',function(err,data){
    if(err){
        //  1. 组织程序的执行
        //  2.把错误消息打印到控制台
        throw error
    }
    console.log(data)
})

fs.readFile ('./data/b.txt','utf-8',function(err,data){
    if(err){
        //  1. 组织程序的执行
        //  2.把错误消息打印到控制台
        throw error
    }
    console.log(data)
})

fs.readFile ('./data/c.txt','utf-8',function(err,data){
    if(err){
        //  1. 组织程序的执行
        //  2.把错误消息打印到控制台
        throw error
    }
    console.log(data)
})
```

通过回调嵌套的方式保证顺序

```js
var fs = require('fs')

fs.readFile ('./data/a.txt','utf-8',function(err,data){
    if(err){
        //  1. 组织程序的执行
        //  2.把错误消息打印到控制台
        throw error
    }
    console.log(data)
    fs.readFile ('./data/b.txt','utf-8',function(err,data){
    if(err){
        //  1. 组织程序的执行
        //  2.把错误消息打印到控制台
        throw error
    }
    console.log(data)
    fs.readFile ('./data/c.txt','utf-8',function(err,data){
    if(err){
        //  1. 组织程序的执行
        //  2.把错误消息打印到控制台
        throw error
    }
    console.log(data)
})
})
})

```

为了解决以上编码方式带来的问题（回调地狱嵌套），所以在Ecmascript6中新增了一个API：`Promise`

- Promise  承诺保证
- Promise本身不是异步，但是内部往往封装一个异步任务

`promise基本语法`

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20211124172408340.png" alt="image-20211124172408340" style="zoom:67%;" />

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20211124173829131.png" alt="image-20211124173829131" style="zoom: 80%;" />

封装`promise`版本的`readfile`

~~~js
var fs = require('fs')

function pReadFile(filepath){
    return new Promise(function(resolve,reject){
        fs.readFile(filepath,'utf-8',function(err,data){
            if(err){
                reject(err)
            }else{
                resolve(data)
            }
        })
    })
}

pReadFile('./data/a.txt')
    .then(function(data){
        console.log(data)
        return pReadFile('./data/b.txt')
    })
    .then(function(data){
        console.log(data)
        return pReadFile('./data/c.txt')
    })
    .then(function(data){
        console.log(data)
    })
~~~

#### 10.3 Generator 生成器函数

async函数

#### 10.4 
