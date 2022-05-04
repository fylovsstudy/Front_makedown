# React 路由

## 1、相关理解

### Ⅰ-SPA的理解

> 1. 单页Web应用（single page web application，SPA）。
> 2. 整个应用只有**一个完整的页面**。
> 3. 点击页面中的链接**不会刷新**页面，只会做页面的**局部更新。**
> 4. 数据都需要通过ajax请求获取, 并在前端异步展现。

### Ⅱ-路由的理解

#### ① 什么是路由?

> 1. 一个路由就是一个映射关系(key:value)
> 2. key为路径, value可能是function或component

#### ② 路由分类

##### 1、后端路由

> 1. 理解： value是function, 用来处理客户端提交的请求。
> 2. 注册路由： router.get(path, function(req, res))
> 3. 工作过程：当node接收到一个请求时, 根据请求路径找到匹配的路由, 调用路由中的函数来处理请求, 返回响应数据

##### 2、前端路由

> 浏览器的历史记录是一个栈的结构，可以通过BOM身上的history对象实现，这就是前端路由的基石。
>
> 这个主要是依靠于history，也就是浏览器的历史记录。
>
> 浏览器上的记录其实就是一个栈，前进一次就是入栈，后退一次就是出栈。
>
> 并且历史记录上有一个监听的方法，可以时时刻刻监听记录的变化。从而判断是否改变路径
>
> [History](https://developer.mozilla.org/zh-CN/docs/Web/API/History)

> 1. 浏览器端路由，value是component，用于展示页面内容。
> 2. 注册路由: `<Route path="/test" component={Test}>`
> 3. 工作过程：当浏览器的path变为/test时, 当前路由组件就会变为Test组件

### Ⅲ-react-router-dom的理解

react的路由有三类：

web【主要适用于前端】,native【主要适用于本地】,anywhere【任何地方】

在这主要使用web也就是这个标题 react-router-dom

**基本的使用：**

- 导航中的a标签改写成Link标签
- < Link to="/路径" >xxx< /Link>
- 展示区写Route标签进行路径的匹配
- < Route path = '/路径' component={组件名称}>
- < App>最外侧包裹了一个< BrowserRouter>或者< HashRouter>

```jsx
<div className="list-group">
    <Link className="list-group-item"  to="/about">About</Link>
    <Link className="list-group-item"  to="/home">Home</Link>
</div>

<div className="panel-body">
    {/* 注册路由，也就是写对应的关系 */}
    <Route path="/about"component={About}/>
    <Route path="/home"component={Home}/>
</div>

index.js:
ReactDOM.render(
    <BrowserRouter>
        <App />
    </BrowserRouter>
    ,document.getElementById("root"))
```

那么使用Link代替a标签之后，在页面上会是什么呢，我们发现其实页面上也是把link转化为了a标签

**路由组件以及一般组件**

1.写法不一样

一般组件：< Demo>

**路由组件：< Route path="/demo" component ={Demo}/>**

2.存放的位置一般不同

一般组件：components

**路由组件：pages**

3.接收的内容【props】

一般组件：写组件标签的时候传递什么，就能收到什么

**路由组件：接收到三个固定的属性【history,location,match】**

```
//三个固定的属性
history:
    go: ƒ go(n)
    goBack: ƒ goBack()
    goForward: ƒ goForward()
    push: ƒ push(path, state)
    replace: ƒ replace(path, state)
location:
    pathname: "/about"
    search: ""
    state: undefined
match:
    params: {}
    path: "/about"
    url: "/about"
```

**Link**

```jsx
<Link className="list-group-item active" to="/about">About</Link>
```

link标签在点击的时候会自动给class添加一个active属性，不适合自定义的属性添加

**NavLink**

因为Link不能够改变标签体，因此只适合用于一些写死的标签。而如果想要有一些点击的效果，使用NavLink.

如下代码，就写了activeClassName，当点击的时候就会触发这个class的样式

```jsx
{/*NavLink在点击的时候就会去找activeClassName="ss"所指定的class的值，如果不添加默认是active
 这是因为Link相当于是把标签写死了，不能去改变什么。*/}
<NavLink activeClassName='offerdao' className="list-group-item " to="/about">About</NavLink>
```

但是可能一个导航又很多标签，如果这样重复的写NavLink也会造成很多的重复性的代码问题。

因此可以对NavLink进行封装：

```jsx
 // 通过{...对象}的形式解析对象，相当于将对象中的属性全部展开
 //<NavLink  to = {this.props.to} children = {this.props.children}/>
<NavLink activeClassName='offerdao' className="list-group-item " {...this.props}></NavLink>
```

在使用的时候：直接写每个标签中不一样的部分就行，比如路径和名称

```jsx
{/*将NavLink进行封装，成为MyNavLink,通过props进行传参数，标签体内容是props的一个特殊的属性，叫做children */}
<MyNavLink to='/about'>About</MyNavLink>
```

**Switch使用**

- 通常情况下，path和component是一一对应的关系
- Switch可以提高路由匹配效率（单一匹配）

```jsx
<Switch>
    <Route path="/about" component={About} />
    <Route path="/home" component={Home} />
    <Route path="/home" component={About} />
</Switch>
```

**样式丢失**

public是脚手架的根路径 如果请求了不存在的资源，就会返回index.html

一开始请求的是以下的地址

```
http://localhost:3000/css/bootstrap.css
```

to加了之后，刷新就会请求以下地址，找不到要求的资源，就返回了index.html

```
http://localhost:3000/offerdao/css/bootstrap.css
```

解决办法：

1. ```jsx
   //public/index.html中引入样式时不写 ./ 写 /(常用)
   <link *rel*="stylesheet" href="./css/bootstrap.css">
   //改为
   <link *rel*="stylesheet" href="/css/bootstrap.css">
   ```

2. ```jsx
   //public/index.html中引入样式时写%PUBLIC_URL%
   <link *rel*="stylesheet" href="%PUBLIC_URL%/css/bootstrap.css">
   %PUBLIC_URL%代表Public的绝对路径
   ```

3. ```jsx
   <BrowserRouter>
   	<App />
   </BrowserRouter>
   #号后面的不会发送给服务器
   ```

**精准匹配和模糊匹配**

- 默认使用的时模糊匹配：【输入的路径】要包含【匹配的路径】，且顺序要一致
- 开启严格匹配：<Route exact ={true} path"/about" component={About}/>
- 严格匹配不要随便开启，需要再开，有时候开启会导致无法继续匹配二级路由

```jsx
//模糊匹配
<MyNavLink to='/home/a/b'>Home</MyNavLink>
<Route path="/home" component={Home} />
//精准匹配 exact="true" 或者 exact
<MyNavLink to='/home/a/b'>Home</MyNavLink>
<Route exact="true" path="/home" component={Home} />
//项目中最好不要开启严格匹配
```

**Redirect**

一般写在所有路由注册的最下方，当所有路由都无法匹配的时候，跳转到Redirect指定的路由

```jsx
 <Switch>
    <Route path="/about" component={About} />
    <Route path="/home" component={Home} />
    <Redirect to="/about" />
    {/* 重定向：没有匹配上的时候去about */}
</Switch>
```

### 嵌套路由

1. 注册子路由的时候要写上父路由的path值
2. 路由的匹配是按照注册路由的顺序进行的

### 路由组件之间的参数传递

三种都需要掌握：

- **params**
- **search**
- **state**

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220408164337457.png" alt="image-20220408164337457" style="zoom: 67%;" />

Message 组件下包含两部分内容：

1. 一个是遍历生成的导航区
2. 另一个是Detail。

在点击不同的链接时，展示不同的Detail，这时候就需要通过导航区的id来判断展示哪一个Detail。

所以需要进行参数的传递

**方法一：params参数**

1. 路由链接（携带参数）： 

   ```jsx
   <Link to={`/demo/test/tom/18`}>
   ```

2. 注册路由（声明接受）

   ```jsx
   <Route path="/demo/test/:name/:age" component={Test}></Route>
   ```

3. 接受参数： `const { name,age } = this.props.match.params`

```jsx
//Message文件
<div>
    <ul>
        {
            messageArr.map((msgObj) => {
                return (
                    <li key={msgObj.id}>
                        {/* 1. 向路由组件传递params参数 */}
                        <Link to={`/home/message/detail/${msgObj.id}/${msgObj.title}`}>{msgObj.title}</Link>&nbsp;&nbsp;
                    </li>
                )
            })
        }
    </ul>
    <hr />
    {/* 2. 声明接受params参数 :id/:title*/}
    <Route path="/home/message/detail/:id/:title" component={Detail}></Route>
</div >
```

```jsx
//Detail文件
render() {
    // 3. Detail组件中接受params参数
    const { id, title } = this.props.match.params
    const findData = data.find((dataObj) => {
        return dataObj.id === id
    })
    return (
        <ul>
            <li>ID:{id}</li>
            <li>TITLE:{title}</li>
            <li>CONTENT:{findData.content}</li>
        </ul>
    )
}
```

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220408164254141.png" alt="image-20220408164254141" style="zoom:80%;" />

**方法二：search参数**

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220409095409095.png" alt="image-20220409095409095" style="zoom:80%;" />

1. 路由链接（携带参数）：

```jsx
<Link to={'/demo/test/?name=tom&age=10'} >  </Link>
```

2. 注册路由（无需声明，正常注册即可）：

```jsx
<Route path="/demo/test" component={Test}></Route>
```

3. 接受参数

```jsx
const {search} = this.props.location
```

备注：接收到的参数search是urlencoded编码字符串，需要借助qs解析，用法如下：

```jsx
import qs from 'qs'
//qs库用法
let obj = { name: 'tom', age: 18 }  //urlencoded: name=tom&age=18  key=value&key=value
qs.stringify(obj)//把对象转成urlencoded

let str = "carName=奔驰&price=199"
qs.parse(str) 
```

**方法三：state参数**

1. 路由链接（携带参数）：

```jsx
<Link to={{path:'/demo/test'}},state={name:'tom',age:19}></Link>
```

2. 注册路由

```jsx
<Route path="/demo/test" component={Test}></Route>
```

3. 接受参数

```jsx
this.props.location.state
//备注：刷新也可以保留参数
```

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220409101421393.png" alt="image-20220409101421393" style="zoom:80%;" />

> 地址栏没有参数，刷新为什么不丢失？
>
> 使用的是browserrouter一致操作的是history.xxxxx。history对象帮我们记着这个。如果缓存清零，就找不到了

**push和replace**

- 默认是push模式
- 开启replace模式

```jsx
replace = {true}
```

**编程式路由导航**

- 不使用Link 和 NavLink 实现跳转
- 主要是借助history API

```
//三个固定的属性
history:
    go: ƒ go(n)
    goBack: ƒ goBack()
    goForward: ƒ goForward()
    push: ƒ push(path, state)
    replace: ƒ replace(path, state)
```

