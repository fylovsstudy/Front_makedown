# 1、AJAX简介

- AJAX全称为Asynchronous JavaScript And XML，就是异步的 JS 和 XML。
- 通过AJAX可以在浏览器中向服务器发送异步请求，最大的优势: 无刷新获取数据。

- AJAX不是新的编程语言，而是一种将现有的标准组合在一起使用的新方式。

# 2、XML简介

XML 可扩展标记语言。

XML 被设计用来传输和存储数据。

XML 和 HTML类似，不同的是HTML中都是预定义标签，而XML中没有预定义标签，全都是自定义标签，用来表示一些数据。

```xml
比如说我有一个学生数据:
	name = "孙悟空",age = 18; gender = "男";

用XML表示:
	<student>
		<name>孙悟空</name>
        <age>18</age>
        <gender>男</gender>
	</student>
```

现在已经被JSON取代了。

```JSON
用JSON表示:
{"name":"孙悟空","age":18,"gender":"男"}
```

# 3、AJAX的特点

## 3.1、AJAX的优点

1. 可以无需刷新页面而与服务器端进行通信。
2. 允许你根据用户事件(鼠标键盘表单。。)来更新部分页面内容。

## 3.2、AJAX的缺点

1. 没有浏览历史，不能回退
2. 存在跨域问题(同源)
3. SEO不友好，(SEO意思: 是搜索引擎优化 search engine optimization)：该数据在响应体中是没有的，通过ajax  动态创建的 通过爬虫不可获取

# 4、HTTP协议请求与响应的结构

HTTP协议【超文本传输协议】，协议详细规定了浏览器和万维网服务器之间互相通信的规则。

- 请求：请求报文
- 响应：响应报文

> 重点是格式和参数

## 4.1、请求报文

**HTTP请求格式**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201119194709328.png#pic_center)

- 行：     请求类型POST...    /  URL      / HTTP1.1 版本  / 
- 头： 
  - Host：atguigu.com
  - Cookie： name=gui
  - Content-type: applocation/x-www-form-urlencoded
  - User-Agent:  chrome 83
- 空行
- 体 :
  -  如果是get请求  请求体是空的  如果是post请求 请求体可以不为空
  - username=admin&password=admin

URL包含: 路径和参数

**请求报文的构成**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201119194718440.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NjMyNjYw,size_16,color_FFFFFF,t_70#pic_center)

如果是GET请求，请求体为空，如果是POST请求，请求体可以不为空。

## 4.2、响应报文

**HTTP响应格式**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201119194725930.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NjMyNjYw,size_16,color_FFFFFF,t_70#pic_center)

**响应报文的构成**

- 行： HTTP/1.1  200  OK

- 头

  - Content-Type: text/html;charset=utf-8
  - Content-length:2048
  - Content-encoding:gzip

- 空行

- 体：

  - ```html
    <html>
        <head>
            ......
        </head>
    </html>
    ```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201119194733289.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NjMyNjYw,size_16,color_FFFFFF,t_70#pic_center)

**详细请看: https://blog.csdn.net/a19881029/article/details/14002273**

# 5 起步

GET.HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AJAX GET 请求</title>
    <style>
        #result{
            width: 200px;
            height: 100px;
            border: solid 1px #90b;
        }
    </style>
</head>
<body>
    <button>点击发送请求</button>
    <div id="result"></div>
</body>
</html>

```

Server.js

```js
// 1.引入express
const express = require('express');
// 2.创建应用对象
const app = express();

// 3.创建路由规则
//request 是对请求报文的封装
//response 是对响应报文的封装
app.get('/server',(request,response)=>{
    //设置响应头
    response.setHeader('Access-Controll-Allow-Origin','*');

    //设置响应体
    response.send('HELLO AJAX');
});

//4.监听端口启动服务
app.listen(8080,()=>{
	console.log("服务已经启动，8080端口监听中.....");
})	

```

## 5.1 GET请求(原生)

GET.HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AJAX GET 请求</title>
    <style>
        #result{
            width: 200px;
            height: 100px;
            border: solid 1px #90b;
        }
    </style>
</head>
<body>
    <button>点击发送请求</button>
    <div id="result"></div>
    <script>
        //获取button元素
        const btn = document.getElementsByTagName('button')[0];
        const result = document.getElementById('result');
        btn.onclick = function(){
           //1.创建对象
           const xhr = new XMLHttpRequest();
           //2.初始化，设置请求方法和url
           xhr.open('GET','http://127.0.0.1:8080/server');
           //3.发送
           xhr.send();
           //4.事件绑定 处理服务端返回的结果
           // readystate 是xhr对象中的属性，表示状态0,1,2,3,4
           /*
                0: 请求未初始化
                1: 服务器连接已建立
                2: 请求已接收
                3: 请求处理中
                4: 请求已完成，且响应已就绪
           */
           xhr.onreadystatechange = function(){
                if(xhr.readyState === 4 && (xhr.status >=200 && xhr.status<300)){
                    // 处理 行 头 空行 体
                    //响应行
                    // console.log(xhr.status);//状态码
                    // console.log(xhr.statusText);//状态字符串
                    // console.log(xhr.getAllResponseHeaders());//所有响应头
                    // console.log(xhr.response);//响应体
                    //设置result的文本
                    result.innerHTML = xhr.response;
                }
           } 
        }
    </script>
</body>
</html>
```

server.js

```js
// 1.引入express
const express = require('express');
// 2.创建应用对象
const app = express();

// 3.创建路由规则
//request 是对请求报文的封装
//response 是对响应报文的封装
app.get('/server',(request,response)=>{
    //设置响应头
    response.setHeader('Access-Control-Allow-Origin','*');

    //设置响应体
    response.send('HELLO AJAX');
});

//4.监听端口启动服务
app.listen(8080,()=>{
	console.log("服务已经启动，8080端口监听中.....");
})
```

## 5.2 post请求（原生）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AJAX 发送POST请求</title>
    <style>
        #result{
            width: 200px;
            height: 100px;
            border: solid 1px #903;
        }
    </style>
</head>
<body>
    <div id="result"></div>
    <script>
        //获取元素对象
        const result = document.getElementById("result");
        //绑定事件
        result.addEventListener("mouseover",function(){
            //1.创建对象
            const xhr = new XMLHttpRequest();
            //2.初始化 设置类型与URL
            xhr.open('POST',"http://127.0.0.1:8000/server");
            //设置请求头信息
             xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded');
            //3.发送
            xhr.send();
            //4.事件绑定
            xhr.onreadystatechange = function(){
                //判断
                if(xhr.readyState === 4){
                    if(xhr.status >= 200 && xhr.status < 300){
                        //处理服务端返回的结果
                        result.innerHTML = xhr.response;
                    }
                }
            }

        });
    </script>
</body>
</html>
```

server.js

```js
// 1.引入express
const express = require('express');
// 2.创建应用对象
const app = express();

// 3.创建路由规则
//request 是对请求报文的封装
//response 是对响应报文的封装
// app.get('/server',(request,response)=>{
//     //设置响应头
//     response.setHeader('Access-Control-Allow-Origin','*');

//     //设置响应体
//     response.send('HELLO AJAX');
// });
app.post('/server',(request,response)=>{
    //设置响应头
    response.setHeader('Access-Control-Allow-Origin','*');

    //设置响应体
    response.send('HELLO AJAX');
});

//4.监听端口启动服务
app.listen(8000,()=>{
	console.log("服务已经启动，8000端口监听中.....");
})
```

## 5.3 服务器响应JSON数据(原生)

JSON.html

JSON: 后端把JSON对象转换为字符串传递给前端，前端通过JSON把传递过来的字符串转换为对象并输出。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JSON响应</title>
    <style>
        #result{
            width:200px;
            height:100px;
            border:solid 1px #89b;
        }
    </style>
</head>
<body>
    <div id="result"></div>
    <script>
        const result = document.getElementById('result');
        //绑定键盘按下事件
        window.onkeydown = function(){
            //发送请求
            const xhr = new XMLHttpRequest();
            //设置响应体数据的类型
            xhr.responseType = 'json';
            //初始化
            xhr.open('GET','http://127.0.0.1:8000/json-server');
            //发送
            xhr.send();
            //事件绑定
            xhr.onreadystatechange = function(){
                if(xhr.readyState === 4){
                    if(xhr.status >= 200 && xhr.status < 300){
                        result.innerHTML = xhr.response.name;
                    }
                }
            }
        }
    </script>
</body>
</html>
```

server.js

```js
// 1.引入express
const express = require('express');
// 2.创建应用对象
const app = express();

// 3.创建路由规则
//request 是对请求报文的封装
//response 是对响应报文的封装
app.get('/server',(request,response)=>{
    //设置响应头
    response.setHeader('Access-Control-Allow-Origin','*');

    //设置响应体
    response.send('HELLO AJAX');
});
// app.post('/server',(request,response)=>{
//     //设置响应头
//     response.setHeader('Access-Control-Allow-Origin','*');

//     //设置响应体
//     response.send('HELLO AJAX');
// });
app.get('/json-server',(request,response)=>{
    //设置响应头
    response.setHeader('Access-Control-Allow-Origin','*');

    //响应一个数据
    const data = {
        name: 'atguigu'
    }
    //把对象转化为json字符串
    let str = JSON.stringify(data);
    //设置响应体
    response.send(data);
});

//4.监听端口启动服务
app.listen(8000,()=>{
	console.log("服务已经启动，8000端口监听中.....");
})
```

## 5.4 IE缓存问题(原生)

IE.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IE缓存问题</title>
    <style>
        #result{
            width:200px;
            height:100px;
            border:solid 1px #258;
        }
    </style>
</head>
<body>
    <button>点击发送请求</button>
    <div id="result"></div>
    <script>
        const btn = document.getElementsByTagName('button')[0];
        const result = document.querySelector('#result');

        btn.addEventListener('click', function(){
            const xhr = new XMLHttpRequest();
            xhr.open("GET",'http://127.0.0.1:8000/ie?time='+Date.now());
            xhr.send();
            xhr.onreadystatechange = function(){
                if(xhr.readyState === 4){
                    if(xhr.status >= 200 && xhr.status< 300){
                        result.innerHTML = xhr.response;
                    }
                }
            }
        })
    </script>
</body>
</html>
```

server.js

```js
// 1.引入express
const express = require('express');
// 2.创建应用对象
const app = express();

// 3.创建路由规则
//request 是对请求报文的封装
//response 是对响应报文的封装
app.get('/server',(request,response)=>{
    //设置响应头
    response.setHeader('Access-Control-Allow-Origin','*');

    //设置响应体
    response.send('HELLO AJAX');
});
// app.post('/server',(request,response)=>{
//     //设置响应头
//     response.setHeader('Access-Control-Allow-Origin','*');

//     //设置响应体
//     response.send('HELLO AJAX');
// });
app.get('/json-server',(request,response)=>{
    //设置响应头
    response.setHeader('Access-Control-Allow-Origin','*');

    //响应一个数据
    const data = {
        name: 'atguigu'
    }
    //对对象进行字符串转换
    let str = JSON.stringify(data);
    //设置响应体
    response.send(data);
});
app.get('/ie',(request,response)=>{
    //设置响应头
    response.setHeader('Access-Control-Allow-Origin','*');

    //设置响应体
    response.send('HELLO IE');
});

//4.监听端口启动服务
app.listen(8000,()=>{
	console.log("服务已经启动，8000端口监听中.....");
})
```

## 5.5 请求异常与网络超时(原生)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>请求超时与异常处理</title>
    <style>
        #result{
            width:200px;
            height:100px;
            border:solid 1px #258;
        }
    </style>
</head>
<body>
    <button>点击发送请求</button>
    <div id="result"></div>
    <script>
        const btn = document.getElementsByTagName('button')[0];
        const result = document.querySelector('#result');

        btn.addEventListener('click', function(){
            const xhr = new XMLHttpRequest();
            //超时设置2s设置
            xhr.timeout = 2000;
            xhr.ontimeout = function(){
                alert('网络异常,请稍后重试');
            }
            //网络异常问题
            xhr.onerror = function(){
                alert('你的网络似乎出了一点问题');
            }
            xhr.open("GET",'http://127.0.0.1:8000/delay');
            xhr.send();
            xhr.onreadystatechange = function(){
                if(xhr.readyState === 4){
                    if(xhr.status >= 200 && xhr.status< 300){
                        result.innerHTML = xhr.response;
                    }
                }
            }
        })
    </script>
</body>
</html>
```

server.js

```js
// 1.引入express
const express = require('express');
// 2.创建应用对象
const app = express();

// 3.创建路由规则
//request 是对请求报文的封装
//response 是对响应报文的封装
app.get('/server',(request,response)=>{
});
//json
app.get('/json-server',(request,response)=>{
});
//ie缓存
app.get('/ie',(request,response)=>{
});
//延迟响应
app.get('/delay',(request,response)=>{
    //设置响应头
    response.setHeader('Access-Control-Allow-Origin','*');
    //定时器
    setTimeout(()=>{
        //设置响应体
    response.send('延时响应');
    },3000)
    
});
//4.监听端口启动服务
app.listen(8000,()=>{
	console.log("服务已经启动，8000端口监听中.....");
})
```

## 5.6 取消发送(原生)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>取消请求</title>
</head>
<body>
    <button>点击发送</button>
    <button>点击取消</button>
    <script>
        //获取元素对象
        const btns = document.querySelectorAll('button');
        
        let x = null;
        btns[0].onclick = function(){
            x = new XMLHttpRequest();
            x.open('GET','http://127.0.0.1:8000/delay');
            x.send();
        }
        btns[1].onclick = function(){
            //abort 中止
            x.abort();
        }
    </script>
</body>
</html>

```

server.js

```js
// 1.引入express
const express = require('express');
// 2.创建应用对象
const app = express();

// 3.创建路由规则
//request 是对请求报文的封装
//response 是对响应报文的封装
app.get('/server',(request,response)=>{
});
//json
app.get('/json-server',(request,response)=>{
});
//ie缓存
app.get('/ie',(request,response)=>{
});
//延迟响应
app.get('/delay',(request,response)=>{
    //设置响应头
    response.setHeader('Access-Control-Allow-Origin','*');
    //定时器
    setTimeout(()=>{
        //设置响应体
    response.send('延时响应');
    },3000)
    
});
//4.监听端口启动服务
app.listen(8000,()=>{
	console.log("服务已经启动，8000端口监听中.....");
})
```

## 5.7 请求重复发送(原生)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>重复请求问题</title>
</head>
<body>
    <button>点击发送</button>
    <script>
        //获取元素对象
        const btns = document.querySelectorAll('button');
        let x = null;
        //标识变量
        let isSending = false; // 是否正在发送AJAX请求

        btns[0].onclick = function(){
            //判断标识变量
            if(isSending) x.abort();// 如果正在发送, 则取消该请求, 创建一个新的请求
            x = new XMLHttpRequest();
            //修改 标识变量的值
            isSending = true;
            x.open("GET",'http://127.0.0.1:8000/delay');
            x.send();
            x.onreadystatechange = function(){
                if(x.readyState === 4){
                    //修改标识变量
                    isSending = false;
                }
            }
        }

        // abort 中止
        btns[1].onclick = function(){
            x.abort();
        }
    </script>
</body>
</html>
```

server.js

```js
// 1.引入express
const express = require('express');
// 2.创建应用对象
const app = express();

// 3.创建路由规则
//request 是对请求报文的封装
//response 是对响应报文的封装
app.get('/server',(request,response)=>{
});
//json
app.get('/json-server',(request,response)=>{
});
//ie缓存
app.get('/ie',(request,response)=>{
});
//延迟响应
app.get('/delay',(request,response)=>{
    //设置响应头
    response.setHeader('Access-Control-Allow-Origin','*');
    //定时器
    setTimeout(()=>{
        //设置响应体
    response.send('延时响应');
    },3000)
    
});
//4.监听端口启动服务
app.listen(8000,()=>{
	console.log("服务已经启动，8000端口监听中.....");
})
```

# 6 JQuery

使用JQuery发送AJAX请求

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>jQuery 发送 AJAX 请求</title>
    <link crossorigin="anonymous" href="https://cdn.bootcss.com/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <script crossorigin="anonymous" src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
</head>
<body>
    <div class="container">
        <h2 class="page-header">jQuery发送AJAX请求 </h2>
        <button class="btn btn-primary">GET</button>
        <button class="btn btn-danger">POST</button>
        <button class="btn btn-info">通用型方法ajax</button>
    </div>
    <script>
        //使用jquery发送get请求
        $('button').eq(0).click(function(){
            $.get('http://127.0.0.1:8000/jquery',{a:100,b:200},function(data){
                console.log(data);
            },'json');
        })
       //使用jquery发送post请求
       $('button').eq(1).click(function(){
            $.post('http://127.0.0.1:8000/jquery',{a:100,b:200},function(data){
                console.log(data);
            },'json');
        })
       //通用方法(开发常用)
       $("button").eq(2).click(function(){
           $.ajax({
               //url
               url: 'http://127.0.0.1:8000/jquery',
               //参数
               data: {a:100,b:200},
               //请求类型
               type: 'GET',
               //响应体结果
               dataType: 'JSON',
               //成功的回调
               success: function(data){
                   console.log(data);
               },
               //超时时间
               timeout: 2000,
               //失败的回调
               error: function(){
                   console.log('出错了');
               },
               //头信息
               headers:{
                   c: 300,
                   d: 400
               }
           })
       })
    </script>
</body>
</html>
```

server.js

```js
// 1.引入express
const express = require('express');
// 2.创建应用对象
const app = express();

// 3.创建路由规则
//request 是对请求报文的封装
//response 是对响应报文的封装
app.get('/server',(request,response)=>{
});
//json
app.get('/json-server',(request,response)=>{
});
//ie缓存
app.get('/ie',(request,response)=>{
});
//延迟响应
app.get('/delay',(request,response)=>{
   
});
//JQuery
app.all('/jquery',(request,response)=>{
    //设置响应头
    response.setHeader('Access-Control-Allow-Origin','*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    const data = {name:'张三'};
    response.send(JSON.stringify(data));
    
});
//4.监听端口启动服务
app.listen(8000,()=>{
	console.log("服务已经启动，8000端口监听中.....");
})

```

# 7 axios

使用axios发送AJAX请求

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>axios 发送 AJAX请求</title>
    <script crossorigin="anonymous" src="https://cdn.bootcdn.net/ajax/libs/axios/0.19.2/axios.js"></script>
</head>

<body>
    <button>GET</button>
    <button>POST</button>
    <button>AJAX</button>

    <script>
        const btns =  document.querySelectorAll('button');
        //配置baseURL
        axios.defaults.baseURL = "http://127.0.0.1:8000";
        btns[0].onclick = function(){
            //GET请求
            axios.get('/axios',{
                //url参数
                params:{
                    id: 100,
                    vip: 7
                },
                //请求头信息
                headers:{
                    name: 'atguigu',
                    age: 20
                }
            }).then(response =>{
                console.log(response)
            })
        }
        //POST请求
        btns[1].onclick = function(){
            axios.post('/axios',{
                username: 'admin',
                password: 'admin',

                //url
                params:{
                    id: 200,
                    vip: 9
                },
                //请求头参数
                headers: {
                    height: 180,
                    weight: 180,
                }
            }).then(response=>{
                console.log(response.data);
                console.log(response.headers);

            })
        }
        //通用方法(开发使用)
        btns[2].onclick = function(){
            axios({
                //请求方法
                method : 'POST',
                //url
                url: '/axios',
                //url参数
                params: {
                    vip:10,
                    level:30
                },
                //头信息
                headers: {
                    a:100,
                    b:200
                },
                //请求体参数
                data: {
                    username: 'admin',
                    password: 'admin'
                }
            }).then(response=>{
                //响应状态码
                console.log(response.status);
                //响应状态字符串
                console.log(response.statusText);
                //响应头信息
                console.log(response.headers);
                //响应体
                console.log(response.data);
            })
        }
    </script>
</body>

</html>
```

server.js

```js
// 1.引入express
const express = require('express');
// 2.创建应用对象
const app = express();

// 3.创建路由规则
//request 是对请求报文的封装
//response 是对响应报文的封装
app.get('/server',(request,response)=>{
});
//json
app.get('/json-server',(request,response)=>{
});
//ie缓存
app.get('/ie',(request,response)=>{
});
//延迟响应
app.get('/delay',(request,response)=>{
   
});
//JQuery
app.all('/jquery',(request,response)=>{

});
//axios
app.all('/axios',(request,response)=>{
    //设置响应头
    response.setHeader('Access-Control-Allow-Origin','*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    const data = {name:'张三'};
    response.send(JSON.stringify(data));
    
});
//4.监听端口启动服务
app.listen(8000,()=>{
	console.log("服务已经启动，8000端口监听中.....");
})
```

# 8 Fetch

fetch 函数：是一个全局对象，返回一个promise对象

![image-20220307221637926](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220307221637926.png)

使用fetch发送AJAX请求

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>fetch 发送 AJAX请求</title>
</head>
<body>
    <button>AJAX请求</button>
    <script>
        const btn = document.querySelector('button');

        btn.onclick = function(){
            fetch('http://127.0.0.1:8000/fetch?vip=10', {
                //请求方法
                method: 'POST',
                //请求头
                headers: {
                    name:'atguigu'
                },
                //请求体
                body: 'username=admin&password=admin'
            }).then(response => {
                // return response.text(); 字符串
                return response.json();  //自动解析成js对象
            }).then(response=>{
                console.log(response);
            });
        }
    </script>
</body>
</html>
```

server.js

```js
// 1.引入express
const express = require('express');
// 2.创建应用对象
const app = express();

// 3.创建路由规则
//request 是对请求报文的封装
//response 是对响应报文的封装
app.get('/server',(request,response)=>{
});
//json
app.get('/json-server',(request,response)=>{
});
//ie缓存
app.get('/ie',(request,response)=>{
});
//延迟响应
app.get('/delay',(request,response)=>{
   
});
//JQuery
app.all('/jquery',(request,response)=>{

});
//axios
app.all('/axios',(request,response)=>{
 
});
//fetch
app.all('/fetch',(request,response)=>{
    //设置响应头
    response.setHeader('Access-Control-Allow-Origin','*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    const data = {name:'张三'};
    response.send(JSON.stringify(data));
    
});
//4.监听端口启动服务
app.listen(8000,()=>{
	console.log("服务已经启动，8000端口监听中.....");
})
```

# 9 跨域

## 9.1 同源策略

- 同源策略是早由Netscape公司提出，是浏览器的一种安全策略。
- 同源: 网页的url和ajax请求目标资源的url  协议、域名、端口号、必须完全相同。
- ajax 默认遵循同源策略，就是说若不同源，则不可以访问
- 违背同源策略就是跨域。

index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>首页</title>
    <script crossorigin="anonymous" src="https://cdn.bootcdn.net/ajax/libs/axios/0.19.2/axios.js"></script>
</head>
<body>
    <h>尚蛙谷</h><br>
    <button>点击获取用户数据</button>
    <script>
        const btn = document.querySelector('button');
        btn.onclick = function(){
            axios({
                method: 'GET',
                url: 'http://127.0.0.1:9000/data'
            }).then(response =>{
                console.log(response.data);
            })
        }
    </script>
</body>
</html>
```

server.js

```js
const express = require('express');

const app = express();

app.get('/home', (request, response)=>{
    //响应一个页面
    response.sendFile(__dirname + '/index.html');
});

app.get('/data', (request, response)=>{
    //防止出现跨域
    response.setHeader('Access-Control-Allow-Origin','*');
    response.send('用户数据');
});

app.listen(9000, ()=>{
    console.log("服务已经启动...");
});
```

## 9.2 如何解决跨域

### 9.2.1、JSONP

1.JSONP是什么

 JSONP（JSON with Padding）是一个非官方的跨域解决方法，纯粹凭借程序员的聪明才智开发出来，只支持get请求。

2.JSONP怎么工作?

 在网页有一些标签天生具有跨域能力，比如: img link iframe script

 JSONP就是利用**script标签的跨域能力**来发送请求的。

3.JSONP的使用

 https://blog.csdn.net/inite/article/details/80333130

原理

html

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>原理演示</title>
    <style>
        #result {
            width: 300px;
            height: 100px;
            border: solid 1px #78a;
        }
    </style>
</head>

<body>
    <div id="result"></div>
    <script>
        //处理数据
        function handle(data) {
            //获取 result 元素
            const result = document.getElementById('result');
            result.innerHTML = data.name;
        }
    </script>
    <!-- <script src="http://127.0.0.1:5500/%E8%AF%BE%E5%A0%82/%E4%BB%A3%E7%A0%81/7-%E8%B7%A8%E5%9F%9F/2-JSONP/js/app.js"></script> -->
    <script src="http://127.0.0.1:8000/jsonp-server"></script>
</body>

</html>
```

server.js

```js
//1. 引入express
const express = require('express');

//2. 创建应用对象
const app = express();

//3. 创建路由规则
// request 是对请求报文的封装
// response 是对响应报文的封装


//jsonp服务
app.all('/jsonp-server',(request, response) => {
    // response.send('console.log("hello jsonp")');
    const data = {
        name: '尚硅谷atguigu'
    };
    //将数据转化为字符串
    let str = JSON.stringify(data);
    //返回结果
    response.end(`handle(${str})`);
});



//4. 监听端口启动服务
app.listen(8000, () => {
    console.log("服务已经启动, 8000 端口监听中....");
});
```

**实践**

html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JSONP实践</title>
</head>
<body>
    用户名<input type="text" id="username"></input>
    <p></p>
    <script>
        //获取input元素
        const input = document.querySelector('input');
        const p = document.querySelector('p');
        //声明handle函数
        function handle(data){
            input.style.border = "solid 1px #f00";
            //修改p标签的提示文本;
            p.innerHTML = data.msg;
        }
        //绑定事件
        input.onblur = function(){
            //获取用户的输入值
            let username = this.value;
            //向服务器端发送请求 检测用户名是否存在
            //1.创建script标签
            const script = document.createElement('script');
            //2.设置标签的src属性
            script.src = "http://127.0.0.1:8000/check";
            //3.将script插入到文档中
            document.body.appendChild(script);
        }
    </script>
</body>
</html>

```

server.js

```js
//1. 引入express
const express = require('express');

//2. 创建应用对象
const app = express();

//3. 创建路由规则
// request 是对请求报文的封装
// response 是对响应报文的封装
//jsonp服务
app.all('/jsonp-server',(request, response) => {
    // response.send('console.log("hello jsonp")');
    const data = {
        name: '尚硅谷atguigu'
    };
    //将数据转化为字符串
    let str = JSON.stringify(data);
    //返回结果
    response.end(`handle(${str})`);
});
//用户名检测是否存在
app.all('/check',(request, response) => {
    // response.send('console.log("hello jsonp")');
    const data = {
        exist: 1,
        msg: '用户名已经存在'
    };
    //将数据转化为字符串
    let str = JSON.stringify(data);
    //返回结果
    response.end(`handle(${str})`);
});


//4. 监听端口启动服务
app.listen(8000, () => {
    console.log("服务已经启动, 8000 端口监听中....");
});
```

**使用jquery完成跨域**

html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>jQuery-jsonp</title>
    <style>
        #result{
            width:300px;
            height:100px;
            border:solid 1px #089;
        }
    </style>
    <script crossorigin="anonymous" src='https://cdn.bootcss.com/jquery/3.5.0/jquery.min.js'></script>
</head>
<body>
    <button>点击发送 jsonp 请求</button>
    <div id="result">

    </div>
    <script>
        $('button').eq(0).click(function(){
            $.getJSON('http://127.0.0.1:8000/jquery-jsonp?callback=?', function(data){
                $('#result').html(`
                    名称: ${data.name}<br>
                    校区: ${data.city}
                `)
            });
        });
    </script>
</body>
</html>
```

server.js

```js
//1. 引入express
const express = require('express');

//2. 创建应用对象
const app = express();

//3. 创建路由规则
// request 是对请求报文的封装
// response 是对响应报文的封装
//jsonp服务
app.all('/jsonp-server',(request, response) => {
    // response.send('console.log("hello jsonp")');
    const data = {
        name: '尚硅谷atguigu'
    };
    //将数据转化为字符串
    let str = JSON.stringify(data);
    //返回结果
    response.end(`handle(${str})`);
});
//用户名检测是否存在
app.all('/check',(request, response) => {
});

app.all('/jquery-jsonp',(request, response) => {
    // response.send('console.log("hello jsonp")');
    const data = {
        name:'尚硅谷',
        city: ['北京','上海','深圳']
    };
    //将数据转化为字符串
    let str = JSON.stringify(data);
    //接收 callback 参数
    let cb = request.query.callback;

    //返回结果
    response.end(`${cb}(${str})`);
});


//4. 监听端口启动服务
app.listen(8000, () => {
    console.log("服务已经启动, 8000 端口监听中....");
});
```

### **9.2.2、CORS**

1.CORS是什么?

**CORS(Cross-Origin Resource Sharing),跨域资源共享**。CORS是官方的跨域解决方案，它的特点是不需要在客户端做任何特殊的操作，完全在服务器中进行处理，支持get和post请求。跨域资源共享标准新增了一组**HTTP首部字段**，允许服务器声明哪些源站通过浏览器有权限访问哪些资源

2.CORS怎么工作?

**CORS是通过设置一个响应头来告诉浏览器，该请求允许跨域**，浏览器收到该响应以后就会对响应执行。

3.CORS的使用

https://blog.csdn.net/qq22692150/article/details/99011726?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control

案例

html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CORS</title>
    <script crossorigin="anonymous" src="https://cdn.bootcdn.net/ajax/libs/axios/0.19.2/axios.js"></script>
    <style>
        #result{
            width:200px;
            height:100px;
            border:solid 1px #90b;
        }
    </style>
</head>
<body>
    <button>发送请求</button>
    <div id="result"></div>
    <script>
        const btn = document.querySelector('button');
        const result = document.getElementById('result');
        btn.onclick = function(){
           axios({
               method: 'GET',
               url: 'http://localhost:8000/cors-server',
           }).then(response =>{
                result.innerHTML = response.data;
           })
        }
    </script>
</body>
</html>

```

server.js

```js
//1. 引入express
const express = require('express');

//2. 创建应用对象
const app = express();

//3. 创建路由规则
// request 是对请求报文的封装
// response 是对响应报文的封装
//jsonp服务
app.all('/jsonp-server',(request, response) => {
});
//用户名检测是否存在
app.all('/check',(request, response) => {
});

app.all('/jquery-jsonp',(request, response) => {
});
app.all('/cors-server', (request, response)=>{
    //设置响应头
    //所有页面都可以跨域访问
    response.setHeader("Access-Control-Allow-Origin", "*");
    //允许发送任意请求头，可以是自定义的
    response.setHeader("Access-Control-Allow-Headers", '*');
    //请求方法任意
    response.setHeader("Access-Control-Allow-Method", '*');
    // response.setHeader("Access-Control-Allow-Origin", "http://127.0.0.1:5500");
    response.send('hello CORS');
});


//4. 监听端口启动服务
app.listen(8000, () => {
    console.log("服务已经启动, 8000 端口监听中....");
});
```

