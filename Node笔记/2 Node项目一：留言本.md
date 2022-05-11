## 1 简单的Apache服务器软件

Apache服务器软件，这个软件默认有一个www目录，所有寻访在www目录中的资源都可以通过网址来浏览

```javascript
//简单的Apache服务器软件
var http = require('http')

var fs = require('fs')

var wwwdir = 'C:/Users/fy/Desktop/web-projects/nodjs/02'

var sever = http.createServer()
//Apache服务器软件，这个软件默认有一个www目录，所有寻访在www目录中的资源都可以通过网址来浏览

//127.0.0.1:80/a.txt
//127.0.0.1:80/index.html
//127.0.0.1:80/apple/login.html
sever.on('request',function(request,response){
  var url = request.url
// /   wwwdir +  index.html
// /a.txt wwwdir +  a.txt
// /apple/login.html  wwwdir + apple/login.html
// /img/a.jpg  wwwdir +  img/a.jpg  
  var path = '/index.html'
  if (url !== '/')
  path = url
  fs.readFile(wwwdir+url,function(err,data){
    if(err)
    return response.end('404 Not Found')
    response.end(data)
  })
//统一处理像apache一样
//return 有两个作用
//  1.方法返回值
//  2.阻止代码继续往后执行 
})

sever.listen('4000',function(){
  console.log('服务器打开')
})
```

## 2 Apache目录列表

### 2.1 替换特殊标记

1. 如何得到wwwdir目录列表中的文件名和目录名：fs.readdir

2. 如何将得到的文件名和目录名替换到template.html中

   2.1 在template.html中需要替换的位置预留一个特殊的标记，就像以前是用模板引擎

   2.2 根据files生成需要的HTML内容

只要做了这两件事，这个问题就解决了

```javascript
var fs = require('fs')
var http = require('http')

var server = http.createServer()

var wwwdir = 'C:/Users/fy/Desktop/web-projects/nodjs/02'
    server.on('request',function(req,res){
        fs.readFile('./template.html',function(err,data){
            if (err)
            return res.end('读取错误')
            fs.readdir(wwwdir,function(err,files){
                if (err)
                return res.end('目录不存在')
        
                var content=''
                files.forEach(function(item){
                    content += `
                    <tr>
                    <td data-value=""><a class="icon file" draggable="true" href="/C:/Users/fy/Desktop/web-projects/nodjs/02/">${item}</a>
                    </td>
                    <td class="detailsColumn" data-value="1001">1001 B</td>
                    <td class="detailsColumn" data-value="1635130358">2021/10/25 上午10:52:38</td>
                    </tr>`
                })
                data = data.toString()
                data = data.replace('*-*',content)
                res.end(data)
            })
        })
        
    })

    server.listen('4000',function(){
        console.log('服务器打开')
    })

```

### 2.2使用模块引擎

#### 2.2.3 模块引擎

-  art-template：art-template 不仅可以在浏览器使用，也可以在node中使用
-  安装  npm install art-template --save
-  该命令在哪执行就会把包下载到哪里，默认会下载到node_module
-   node_modules不要改，也不支持改

#### 2.2.4 模板引擎使用

1. 安装npm install art-template

2. 在需要使用的文件模板中加载art-template

   只需要使用require方式加载

   参数中的art-template就是你下载的包的名字

   也就是你install的名字是什么，则你require中的就是什么

3. 查文档，使用模板引擎的API

```javascript
//浏览器中使用模板引擎
var fs = require('fs')

var template = require('art-template')

fs.readFile('./tpl.html', function (err, data) {
    if (err) {
      return console.log('读取文件失败了')
    }
    // 默认读取到的 data 是二进制数据
    // 而模板引擎的 render 方法需要接收的是字符串
    // 所以我们在这里需要把 data 二进制数据转为 字符串 才可以给模板引擎使用
    var ret = template.render(data.toString(), {
      name: 'Jack',
      age: 18,
      province: '北京市',
      hobbies: [
        '写代码',
        '唱歌',
        '打游戏'
      ],
      title: '个人信息'
    })
  
    console.log(ret)
})

```

```javascript
//Apache服务中使用模板引擎
var fs = require('fs')
var http = require('http')

var server = http.createServer()

var template = require('art-template')

var wwwdir = 'C:/Users/fy/Desktop/web-projects/nodjs/02'
    server.on('request',function(req,res){
        fs.readFile('./template-apache.html',function(err,data){
            if (err)
            return res.end('读取错误')
            fs.readdir(wwwdir,function(err,files){
                if (err)
                return res.end('目录不存在')
                
                var ret_html = template.render(data.toString(),{
                files:files
                })                
                res.end(ret_html)
            })
        })  
    })

    server.listen('4000',function(){
        console.log('服务器打开')
})
```

## 3 留言网页

```javascript
// app application 应用程序
// 把当前模块所有的依赖项都声明再文件模块最上面
// 为了让目录结构保持统一清晰，所以我们约定，把所有的 HTML 文件都放到 views（视图） 目录中
// 我们为了方便的统一处理这些静态资源，所以我们约定把所有的静态资源都存放在 public 目录中
// 哪些资源能被用户访问，哪些资源不能被用户访问，我现在可以通过代码来进行非常灵活的控制
// /public 整个 public 目录中的资源都允许被访问
// 前后端融会贯通了，为所欲为

var http = require('http')

var url = require('url')

var fs = require('fs')

var template = require('art-template')

var comments=[
    {
        name:'张三',
        message:'今天天气不错',
        datatime:'2015-10-16'
    },
    {
        name:'李四',
        message:'今天天气不错',
        datatime:'2015-10-16'
    },
    {
        name:'王二麻子',
        message:'今天天气不错',
        datatime:'2015-10-16'
    }
]
// /pinglun?name=的撒的撒&message=的撒的撒的撒
// 对于这种表单提交的请求路径，由于其中具有用户动态填写的内容
// 所以你不可能通过去判断完整的 url 路径来处理这个请求
// 
// 结论：对于我们来讲，其实只需要判定，如果你的请求路径是 /pinglun 的时候，那我就认为你提交表单的请求过来了

//var wwwdir='C:\Users\fy\Desktop\web-projects\nodjs\02\feedback\views'
http
    .createServer(function(req,res){
        // 使用url.parse方法将路径解析为一个方便操作的对象，true表示直接将查询字符串转为对象，通过Query属性访问
        var parseObj = url.parse(req.url,true)

        //单独获取不包含查询字符串的路径部分(该路径不包含?之后的内容)
        var pathname  = parseObj.pathname
        
        if (pathname==='/'){
            fs.readFile('./views/index.html',function(err,data){
                if(err)
                return res.end('Fail') 
                
                var html_string = template.render(data.toString(),{
                    comments:comments
                })
                res.end(html_string)
            })
        }else if (pathname==='/post'){
            fs.readFile('./views/post.html',function(err,data){
                if (err)
                return res.end('false reading post.html')
                res.end(data)
            })
        } 
        else if (pathname.indexOf('/public/')===0){
                console.log(pathname)
                fs.readFile('.'+pathname,function(err,data){
                if (err)
                {return res.end('404 Not Found')}
                res.end(data)
            })
        } else if (pathname ==='/pinglun'){
            console.log(pathname)
            // 这个时候无论/pinglun？之后是什么，都不用担心，因为我的pathname不包含?之后的内容
            console.log('收到表单请求了',parseObj.query)

            // res.end(JSON.stringify(parseObj.query))
            // 我们已经使用 url 模块的 parse 方法把请求路径中的查询字符串给解析成一个对象了
            // 所以接下来要做的就是：
            //    1. 获取表单提交的数据 parseObj.query
            //    2. 将当前时间日期添加到数据对象中，然后存储到数组中
            //    3. 让用户重定向跳转到首页 /
            //       当用户重新请求 / 的时候，我数组中的数据已经发生变化了，所以用户看到的页面也就变了
            var comment = parseObj.query
            comment.datatime = '2021-10-25'
            comments.push(comment)
            // unshift    push
            
            // 服务端这个时候已经把数据存储好了，接下来就是让用户重新请求 / 首页，就可以看到最新的留言内容了
            
            // 如何通过服务器让客户端重定向？
            //    1. 状态码设置为 302 临时重定向
            //        statusCode
            //    2. 在响应头中通过 Location 告诉客户端往哪儿重定向
            //        setHeader
            // 如果客户端发现收到服务器的响应的状态码是 302 就会自动去响应头中找 Location ，然后对该地址发起新的请求
            // 所以你就能看到客户端自动跳转了
            res.statusCode = 302
            res.setHeader('Location','/')
            res.end()
        }
        else{
            res.end('404 Not Found')
        }
    })
    .listen('4000',function(){
        console.log('服务器运行')
    })
    
// 晚上写案例照着下面的步骤写：
// 1. / index.html
// 2. 开放 public 目录中的静态资源
//    当请求 /public/xxx 的时候，读取响应 public 目录中的具体资源
// 3. /post post.html
// 4. /pinglun
//    4.1 接收表单提交数据
//    4.2 存储表单提交的数据
//    4.3 让表单重定向到 /
//        statusCode
//        setHeader
```

```HTML
<html lang="en"><head>
    <meta charset="UTF-8">
    <title>留言本</title>
    <!-- 
      浏览器收到 HTML 响应内容之后，就要开始从上到下依次解析，
      当在解析的过程中，如果发现：
        link
        script
        img
        iframe
        video
        audio
        等带有 src 或者 href（link） 属性标签（具有外链的资源）的时候，浏览器会自动对这些资源发起新的请求。
     -->
     <!-- 
        注意：在服务端中，文件中的路径就不要去写相对路径了。
        因为这个时候所有的资源都是通过 url 标识来获取的
        我的服务器开放了 /public/ 目录
        所以这里的请求路径都写成：/public/xxx
        / 在这里就是 url 根路径的意思。
        浏览器在真正发请求的时候会最终把 http://127.0.0.1:3000 拼上
  
        不要再想文件路径了，把所有的路径都想象成 url 地址
      -->
    <link rel="stylesheet" href="/public/lib/bootstrap/bootstrap.css">
  </head>
  
  <body>
    <div class="header container">
      <div class="page-header">
        <h1>Example page header <small>Subtext for header</small></h1>
        <!-- <a> 标签定义超链接，用于从一张页面链接到另一张页面。 -->
        <!-- <a> 元素最重要的属性是 href 属性，它指示链接的目标。 -->
        <a class="btn btn-success" href="/post">发表留言</a>
      </div>
    </div>
    <div class="comments container">
      <ul class="list-group">
      {{each comments}}
        <li class="list-group-item">{{ $value.name}}说：{{$value.message}}<s class="pull-right">{{$value.datatime}}</s></li>
      {{/each}}
      </ul>
    </div>
<!--     <script src="/public/js/main.js"></script>
    <script src="/public/css/main.css"></script>
    <img src="/public/img"> 
-->
  </body>
</html>
```

![image-20211026160108612](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20211026160108612.png)

### 4 Node Server

![image-20211026155130117](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20211026155130117.png)

- 设计好url地址，设计好这个规则，让用户按照你的规则来访问