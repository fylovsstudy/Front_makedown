1 React简介

**react是什么？**

React用于构建用户界面的JS库。**是一个将数据渲染为HTML视图的开源JS库**。

**为什么学？**

1.原生JS操作DOM繁琐，效率低

2.使用JS直接操作DOM,浏览器会进行大量的重绘重排

3.原生JS没有**组件化**编码方案，代码复用低

**React特点**

1. 采用**组件化**模块、**声明式编码**（原生是命令式，不能少任何一步），提高开发效率和组件复用率
2. 在React Native 中可以使用React语法进行**移动端开发**
3. 使用**虚拟DOM**+优秀的**Diffing算法**，尽量减少与真实DOM的交互
   - React会进行虚拟DOM的比较，如果和之前的一样，则不会生成新的真实DOM

![image-20220312231644194](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220312231644194.png)

**学习React需要的JS知识**

- 判断this的指向
- class（类）
- ES6语法规范
- npm包管理器
- 原型、原型链
- 数组常用方法
- 模块化

## React 基础案例

1.先倒入三个包：

【先引入react.development.js，后引入react-dom.development.js】

```js
react.development.js
react-dom.development.js
babel.min.js 
```

2.创建一个容器

3.创建虚拟DOM，渲染到容器中

```js
<body>
    <!-- 准备好容器 -->
    <div id="test">

    </div>
</body>
<!-- 引入依赖 ,引入的时候，必须就按照这个步骤-->
<script src="../js/react.development.js" type="text/javascript"></script>
<script src="../js/react-dom.development.js" type="text/javascript"></script>

<script src="../js/babel.min.js" type="text/javascript"></script>

<!--这里使用了babel用来解析jsx语法-->
<script type="text/babel">
        // 1.创建虚拟DOM
        const VDOM = <h1>Hello</h1>  //这个地方使用的是JSX语法，不需要加""
        // 2.渲染，如果有多个渲染同一个容器，后面的会将前面的覆盖掉
        ReactDOM.render(VDOM,document.getElementById("test"));        
</script>
</html>
```

这样，就会在页面中的这个div容器上添加这个h1.

实例如下：

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220313092311195.png" alt="image-20220313092311195" style="zoom: 80%;" />

## JSX基础语法

1.定义虚拟DOM，不能使用“”

2.**标签中混入JS表达式的时候使用{}**  **注意是表达式！不是JS代码和语句！**

3.样式的类名指定不要使用class，使用className

4.内联样式要使用双大括号包裹

5.不能有多个根标签，只能有一个跟标签

6.标签必须闭合

7.标签首字母：

- 如果小写字母开头，就将标签转化为html同名元素
- 如果html中无该标签对应的元素，就报错；
- 如果是大写字母开头，react就去渲染对应的组件，如果没有就报错

实例如下：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .test {
            width: 90px;
            height: 20px;
            background-color: antiquewhite;
        }
    </style>
</head>

<body>
    <!-- 准备好一个容器-->
    <div id="test"></div>

    <!-- 引入react核心库 -->
    <script type="text/javascript" src="../jss/react.development.js"></script>
    <!-- 引入react-dom，用于支持react操作dom -->
    <script type="text/javascript" src="../jss/react-dom.development.js"></script>
    <!-- 引入babel，用于将jsx转为js -->
    <script type="text/javascript" src="../jss/babel.min.js"></script>

    <script type="text/babel">
        const myID = 'Title'
        const myData = 'Hello'
        //  1. 创建虚拟DOM 
        const VDOM = ( // 此处一定不要写引号，因为不是字符串 
            <div id="title">
                <h1 className="test" id={myID.toLowerCase()}>
                    < span style={{ color: 'red', fontSize: '29px' }}> {myData.toUpperCase()}</span >
                </h1 >
                <h1 id={myID.toUpperCase()}>
                    < span > {myData.toUpperCase()}</span >
                </h1 >
                <input type="text" />

            </div>
        )
        //  2. 渲染虚拟DOM到页面 
        ReactDOM.render(VDOM, document.getElementById('test'))
        /*
        JSX语法规则
         */
    </script>
</body>

</html>
```

### 小练习

**注意：**

1. 一定注意区分JS语句与JS表达式的区别
               1. 一个表达式会产生一个值，可以放在任何一个需要值额地方
                   下面这些都是表达式 
                   (1)  a
                   (2) a+b
                   (3) demo(1)这是函数调用表达式
                   (4) arr.map()  也是表达式
                       let arr = [1,3,5,7,9]
                       const result = arr.map((num) => {
                           return num + 1 
                       })
                       map() 方法创建一个新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值。
                   (5) function () {  } 也是
                       const x = function () {

​                }就是函数本身
​        2.语句（代码）
​                下面这些都是语句
​                (1) if() {}
​                (2) for() {}
​                (3) switch () {case:xxx}

​        const x= 能接到值就是表达式！

2.  react  不会自动遍历对象！但是可以自动遍历数组

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .test {
            width: 90px;
            height: 20px;
            background-color: antiquewhite;
        }
    </style>
</head>

<body>
    <!-- 准备好一个容器-->
    <div id="test"></div>

    <!-- 引入react核心库 -->
    <script type="text/javascript" src="../jss/react.development.js"></script>
    <!-- 引入react-dom，用于支持react操作dom -->
    <script type="text/javascript" src="../jss/react-dom.development.js"></script>
    <!-- 引入babel，用于将jsx转为js -->
    <script type="text/javascript" src="../jss/babel.min.js"></script>

    <script type="text/babel">
        /*
        一定注意区分JS语句与JS表达式的区别
            1. 一个表达式会产生一个值，可以放在任何一个需要值额地方
                下面这些都是表达式 
                (1)  a
                (2) a+b
                (3) demo(1)这是函数调用表达式
                (4) arr.map()  也是表达式
                    let arr = [1,3,5,7,9]
                    const result = arr.map((num) => {
                        return num + 1 
                    })
                    map() 方法创建一个新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值。
                (5) function () {  } 也是
                    const x = function () {

                    }就是函数本身
            2.语句（代码）
                    下面这些都是语句
                    (1) if() {}
                    (2) for() {}
                    (3) switch () {case:xxx}

            const x= 能接到值就是表达式！
         */
        // 模拟一些数据
        const data = ['Angular', 'React', 'Vue']
        // react  不会自动遍历对象！
        // 创建一个虚拟DOM
        const VDOM = (
            <div>
                <h1 className="title"> 前端JS框架  </h1>
                {data.map((item, index) => {
                    return <li key={index}>{item}</li>
                })}
            </div>

        )

        ReactDOM.render(VDOM, document.getElementById('test'))
    </script>
</body>

</html>
```

## 两种创建虚拟DOM的方式

**1.使用JSX创建虚拟DOM**

```html
 const VDOM = (
            <h1 id = {MyId.toLocaleUpperCase()}>
                <span className = "sss" style = {{fontSize:'50px'}}>sss</span>
            </h1>
        )
```

这个在上面的案例中已经演示过了 ，下面看看另外一种创建虚拟DOM的方式

**2.使用JS创建虚拟DOM**

```html
// 1.创建虚拟DOM[在这使用了js的语法]React.createElement(标签,标签属性,内容)
const VDOM = React.createElement('h1',{id:"title"},"nihao")
```

使用JS和JSX都可以创建虚拟DOM，但是可以看出JS创建虚拟DOM比较繁琐，尤其是标签如果很多的情况下，所以还是比较推荐使用JSX来创建。

## 模块与组件、模块化与组件化的理解

**模块**

理解：向外提供特定功能的js程序, 一般就是一个js文件

为什么要拆成模块：随着业务逻辑增加，代码越来越多且复杂。

作用：复用js, 简化js的编写, 提高js运行效率

**组件**

- 当应用是以多组件的方式实现，这个应用就是一个组件化的应用
- 所有实现功能的代码加资源的集合，包括html css js img video font
- 作用是：复用代码，提高运行效率

> **注意：** 组件名称必须以大写字母开头。
>
> React 会将以小写字母开头的组件视为原生 DOM 标签。例如，< div />`代表 HTML 的 div 标签，而`< Weclome /> 则代表一个组件，并且需在作用域内使用 `Welcome`
>
> 传递的参数，不能在组件中改动

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220313102234756.png" alt="image-20220313102234756" style="zoom:80%;" />

**模块化**

当应用的js都以模块来编写的, 这个应用就是一个模块化的应用

**组件化**

当应用是以多组件的方式实现, 这个应用就是一个组件化的应用

**工程化**



# 2 React面向组件编程

## [函数式组件](D:\Workspace\Web\React\react_basic\05_react组件\1_函数式组件.html)

**函数式组件定义：**

1. 创建函数式组件

- 这是一个函数 但是没有被我们调用，是React帮助我们调用的
- this？ undefined 是由于babel编译后开启了严格模式，严格模式下禁止自定义函数下的this指向	windows
- 定义函数式组件的时候要用大写！
- 函数必须要有返回值

2. 执行了ReactDOM之后发生了什么

​    1. React解析组件标签，找到了MyComponent组件

​    2. 发现组件是使用函数定义的，随后调用该函数，将返回的虚拟DOM 转为真实DOM，随后呈现在页面中

## [类的复习](D:\Workspace\Web\React\react_basic\复习\1_类的基本知识.html)

## Class组件

```jsx
//必须继承React.Component
//然后重写Render()方法，该方法一定要有返回值，返回一个虚拟DOM
//this 指向的是MyComponent的实例对象 组件实例对象
class MyComponent extends React.Component {
    render() {
        return <h2>我是复杂组件</h2>
    }
}
ReactDOM.render(<MyComponent/>,document.getElementById('test'))
```

执行过程：

 **1.React解析组件标签，找到相应的组件**

 **2.发现组件是类定义的，随后new出来的类的实例，并通过该实例调用到原型上的render方法**

 **3.将render返回的虚拟DOM转化为真实的DOM,随后呈现在页面中**

**复杂组件和简单组件：是否有状态state，组件的状态里面存放的数据，数据的改变会影响真实的DOM，状态是组件实例对象上面的**

## 组件案例

# 3 组件实例的三大属性

> 就是通过类定义的组件

## state

我们都说React是一个状态机，体现是什么地方呢，就是体现在state上，通过与用户的交互，实现不同的状态，然后去渲染UI,这样就让用户的数据和界面保持一致了。state是组件的私有属性。

在React中，更新组件的state，结果就会重新渲染用户界面(不需要操作DOM),一句话就是说，用户的界面会随着状态的改变而改变。

state是组件对象最重要的属性，值是对象（可以包含多个key-value的组合）

**案例**：

1.需求：页面显示【今天天气很炎热】，鼠标点击文字的时候，页面更改为【今天天气很凉爽】

核心代码如下：

```
<body>
    <!-- 准备好容器 -->
    <div id="test">
        
    </div>
</body>
<!-- 引入依赖 ,引入的时候，必须就按照这个步骤-->
<script src="../js/react.development.js" type="text/javascript"></script>
<script src="../js/react-dom.development.js" type="text/javascript"></script>

<script src="../js/babel.min.js"></script>
<!--这里使用了js来创建虚拟DOM-->
<script type="text/babel">
        //1.创建组件
        class St extends React.Component{
            constructor(props){
                super(props);
                //先给state赋值
                this.state = {isHot:true,win:"ss"};
                //找到原型的dem，根据dem函数创建了一个dem1的函数，并且将实例对象的this赋值过去
                this.dem1 = this.dem.bind(this);
            }
            //render会调用1+n次【1就是初始化的时候调用的，n就是每一次修改state的时候调用的】
            render(){ //这个This也是实例对象
                //如果加dem()，就是将函数的回调值放入这个地方
                //this.dem这里面加入this，并不是调用，只不过是找到了dem这个函数，在调用的时候相当于直接调用，并不是实例对象的调用
                return <h1 onClick = {this.dem1}>今天天气很{this.state.isHot?"炎热":"凉爽"}</h1>    
            }
            //通过state的实例调用dem的时候，this就是实例对象
            dem(){
                const state =  this.state.isHot;
                 //状态中的属性不能直接进行更改，需要借助API
                // this.state.isHot = !isHot; 错误
                //必须使用setState对其进行修改，并且这是一个合并
                this.setState({isHot:!state});
            }
        }
        // 2.渲染，如果有多个渲染同一个容器，后面的会将前面的覆盖掉
        ReactDOM.render(<St />,document.getElementById("test"));
</script>
```

需要注意的是：

1.组件的构造函数，必须要传递一个props参数

2.特别关注this【重点】，类中所有的方法局部都开启了严格模式，如果直接进行调用，this就是undefined

3.想要改变state,需要使用setState进行修改，如果只是修改state的部分属性，则不会影响其他的属性，这个只是合并并不是覆盖。

this.setState()，该方法接收两种参数：对象或函数。

1. 对象：即想要修改的state
2. 函数：接收两个函数，第一个函数接受两个参数，第一个是当前state，第二个是当前props，该函数返回一个对象，和直接传递对象参数是一样的，就是要修改的state；第二个函数参数是state改变后触发的回调

在此还需要注意的是，setState有异步更新和同步更新两种形式，那么什么时候会同步更新，什么时候会异步更新呢？

**React控制之外的事件中调用setState是同步更新的。比如原生js绑定的事件，setTimeout/setInterval等**。

**大部分开发中用到的都是React封装的事件，比如onChange、onClick、onTouchMove等，这些事件处理程序中的setState都是异步处理的。**

```
//1.创建组件
class St extends React.Component{
    //可以直接对其进行赋值
    state = {isHot:10};
    render(){ //这个This也是实例对象
        return <h1 onClick = {this.dem}>点击事件</h1> 
    }
//箭头函数 [自定义方法--->要用赋值语句的形式+箭头函数]
    dem = () =>{
        //修改isHot
        this.setState({ isHot: this.state.isHot + 1})
        console.log(this.state.isHot);
    }
}
```

上面的案例中预期setState使得isHot变成了11，输出也应该是11。然而在控制台打印的却是10，也就是并没有对其进行更新。这是因为异步的进行了处理，在输出的时候还没有对其进行处理。

```
componentDidMount(){
    document.getElementById("test").addEventListener("click",()=>{
        this.setState({isHot: this.state.isHot + 1});
        console.log(this.state.isHot);
    })
}
```

但是通过这个原生JS的，可以发现，控制台打印的就是11，也就是已经对其进行了处理。也就是进行了同步的更新。

**React怎么调用同步或者异步的呢？**

在 React 的 setState 函数实现中，会根据一个变量 isBatchingUpdates 判断是直接更新 this.state 还是放到队列中延时更新，而 isBatchingUpdates 默认是 false，表示 setState 会同步更新 this.state；但是，有一个函数 batchedUpdates，该函数会把 isBatchingUpdates 修改为 true，而当 React 在调用事件处理函数之前就会先调用这个 batchedUpdates将isBatchingUpdates修改为true，这样由 React 控制的事件处理过程 setState 不会同步更新 this.state。

**如果是同步更新，每一个setState对调用一个render，并且如果多次调用setState会以最后调用的为准，前面的将会作废；如果是异步更新，多个setSate会统一调用一次render**

```
dem = () =>{
    this.setState({
        isHot:  1,
        cont:444
    })
    this.setState({
    	isHot: this.state.isHot + 1

    })
    this.setState({
        isHot:  888,
        cont:888
    })
}
```

上面的最后会输出：isHot是888，cont是888

```
 dem = () =>{
                
                this.setState({
                    isHot: this.state.isHot + 1,
                    
                })
                this.setState({
                    isHot: this.state.isHot + 1,
                    
                })
                this.setState({
                    isHot: this.state.isHot + 888
                })
            }
```

初始isHot为10，最后isHot输出为898，也就是前面两个都没有执行。

**注意！！这是异步更新才有的，如果同步更新，每一次都会调用render，这样每一次更新都会 **

**简化版本：**

1.state的赋值可以不再构造函数中进行

2.使用了箭头函数，将this进行了改变

```
<body>
    <!-- 准备好容器 -->
    <div id="test">
        
    </div>
</body>
<!-- 引入依赖 ,引入的时候，必须就按照这个步骤-->
<script src="../js/react.development.js" type="text/javascript"></script>
<script src="../js/react-dom.development.js" type="text/javascript"></script>

<script src="../js/babel.min.js"></script>
<script type="text/babel">
        class St extends React.Component{
            //可以直接对其进行赋值
            state = {isHot:true};
            render(){ //这个This也是实例对象
                return <h1 onClick = {this.dem}>今天天气很{this.state.isHot?"炎热":"凉爽"}</h1>    
                //或者使用{()=>this.dem()也是可以的}
            }
            //箭头函数 [自定义方法--->要用赋值语句的形式+箭头函数]
            dem = () =>{
                console.log(this);
                const state =  this.state.isHot;
                this.setState({isHot:!state});
            }
        }
        ReactDOM.render(<St />,document.getElementById("test"));       
</script>
```

如果想要在调用方法的时候传递参数，有两个方法：

```
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

上述两种方式是等价的，分别通过[箭头函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)和 [`Function.prototype.bind`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind) 来实现。

在这两种情况下，React 的事件对象 `e` 会被作为第二个参数传递。如果通过箭头函数的方式，事件对象必须显式的进行传递，而通过 `bind` 的方式，事件对象以及更多的参数将会被隐式的进行传递。D:\Workspace\Web\React\react_basic\06_组件实例三大属性\2_state精简.html)

## Props ——保存标签属性(只读)

### props基本使用

```jsx
//创建组件
		class Person extends React.Component{
			render(){
				// console.log(this);
				const {name,age,sex} = this.props
				return (
					<ul>
						<li>姓名：{name}</li>
						<li>性别：{sex}</li>
						<li>年龄：{age+1}</li>
					</ul>
				)
			}
		}
		//渲染组件到页面
		ReactDOM.render(<Person name="jerry" age={19}  sex="男"/>,document.getElementById('test1'))
		ReactDOM.render(<Person name="tom" age={18} sex="女"/>,document.getElementById('test2'))

		const p = {name:'老刘',age:18,sex:'女'}
		// console.log('@',...p);
		// ReactDOM.render(<Person name={p.name} age={p.age} sex={p.sex}/>,document.getElementById('test3'))
		ReactDOM.render(<Person {...p}/>,document.getElementById('test3'))
```

### 对标签属性做限制

```jsx
//创建组件
		class Person extends React.Component {
			render() {
				// console.log(this);
				const { name, age, sex } = this.props
				//props是只读的
				//this.props.name = 'jack' //此行代码会报错，因为props是只读的
				return (
					<ul>
						<li>姓名：{name}</li>
						<li>性别：{sex}</li>
						<li>年龄：{age + 1}</li>
					</ul>
				)
			}
		}
		//对标签属性进行类型、必要性的限制
		Person.propTypes = {
			name: PropTypes.string.isRequired, //限制name必传，且为字符串
			sex: PropTypes.string,//限制sex为字符串
			age: PropTypes.number,//限制age为数值
			speak: PropTypes.func,//限制speak为函数
		}
		//指定默认标签属性值
		Person.defaultProps = {
			sex: '男',//sex默认值为男
			age: 18 //age默认值为18
		}
		//渲染组件到页面
		ReactDOM.render(<Person name={100} speak={speak} />, document.getElementById('test1'))
		ReactDOM.render(<Person name="tom" age={18} sex="女" />, document.getElementById('test2'))
		// age = {18} 传递的就是number

		const p = { name: '老刘', age: 18, sex: '女' }
		// console.log('@',...p);
		// ReactDOM.render(<Person name={p.name} age={p.age} sex={p.sex}/>,document.getElementById('test3'))
		ReactDOM.render(<Person {...p} />, document.getElementById('test3'))

		function speak() {
			console.log('我说话了');
		}
```

### props简写

```jsx
//创建组件
class Person extends React.Component{

    constructor(props){
        //构造器是否接收props，是否传递给super，取决于：是否希望在构造器中通过this访问props
        // console.log(props);
        super(props)
        console.log('constructor',this.props);
    }

    //static 是给类本身加了属性  而不是给类的实例加
    ///静态方法不能在对象上调用，只能在类中调用。
    //对标签属性进行类型、必要性的限制
    static propTypes = {
        name:PropTypes.string.isRequired, //限制name必传，且为字符串
        sex:PropTypes.string,//限制sex为字符串
        age:PropTypes.number,//限制age为数值
    }

    //指定默认标签属性值
    static defaultProps = {
        sex:'男',//sex默认值为男
        age:18 //age默认值为18
    }

    render(){
        // console.log(this);
        const {name,age,sex} = this.props
        //props是只读的
        //this.props.name = 'jack' //此行代码会报错，因为props是只读的
        return (
            <ul>
                <li>姓名：{name}</li>
                <li>性别：{sex}</li>
                <li>年龄：{age+1}</li>
            </ul>
        )
    }
}

//渲染组件到页面
ReactDOM.render(<Person name="jerry"/>,document.getElementById('test1'))
```

### 构造器

- 构造器是否接收props，是否传递给super，取决于：是否希望在构造器中**通过this访问props**
- 构造器的使用场景：
  - 为事件处理函数绑定实例
    - 可以通过自定义方法————赋值语句+箭头函数
  - 初始化state的状态
    - 可以在constructor 外部定义
- 如果要写构造函数就一定要写super

### 函数组件使用props

```jsx
//创建组件
		function Person (props){
			const {name,age,sex} = props
			return (
					<ul>
						<li>姓名：{name}</li>
						<li>性别：{sex}</li>
						<li>年龄：{age}</li>
					</ul>
				)
		}
		Person.propTypes = {
			name:PropTypes.string.isRequired, //限制name必传，且为字符串
			sex:PropTypes.string,//限制sex为字符串
			age:PropTypes.number,//限制age为数值
		}

		//指定默认标签属性值
		Person.defaultProps = {
			sex:'男',//sex默认值为男
			age:18 //age默认值为18
		}
		//渲染组件到页面
		ReactDOM.render(<Person name="jerry"/>,document.getElementById('test1'))
```

## refs

### 字符串形式的refs

```jsx
//创建组件
		class Demo extends React.Component{
			//展示左侧输入框的数据
			showData = ()=>{
				const {input1} = this.refs
				alert(input1.value)
			}
			//展示右侧输入框的数据
			showData2 = ()=>{
				const {input2} = this.refs
				alert(input2.value)
			}
			render(){
				return(
					<div>
						<input ref="input1" type="text" placeholder="点击按钮提示数据"/>&nbsp;
						<button onClick={this.showData}>点我提示左侧的数据</button>&nbsp;
						<input ref="input2" onBlur={this.showData2} type="text" placeholder="失去焦点提示数据"/>
					</div>
				)
			}
		}
		//渲染组件到页面
		ReactDOM.render(<Demo a="1" b="2"/>,document.getElementById('test'))
```

### [什么时候可以省略ref](D:\Workspace\Web\React\react_basic\09_react事件处理\事件处理.html)

发生事件的结点和操作的结点是一个的时候

### 非受控组件和受控组件

# 4 组件的生命周期

- render() 调用的时机有俩：初始化渲染和状态更新
- componentDidMount() :**组件挂载完毕的时候调用**
- componentWillUnmount():组件将要卸载的时候调用

> unmountComponentAtNode(document.getElementById(''))是把组件卸载

引出了生命周期回调函数 《=》 生命周期钩子函数

### 4.1 理解

- 组件从创建到死亡它会经历一些特定的阶段。
- React组件中包含一系列勾子函数(生命周期回调函数), 会在特定的时刻调用。
- 我们在定义组件时，会在特定的生命周期回调函数中，做特定的工作。

![image-20220315224025037](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220315224025037.png)

### 4.2 旧生命周期的总结

**1.** **初始化阶段:** 由ReactDOM.render()触发---**初次渲染**

- constructor()
- componentWillMount()
- render()
- **componentDidMount()**：常用
  - 组件挂载完毕的钩子
  - 一般在这个钩子中做一些初始化的事情：例如开启定时器、发送网络请求、订阅消息

​    **2.** **更新阶段:** 由**组件内部this.setState()**或**父组件重新render触发**

- shouldComponentUpdate()
- componentWillUpdate()
- **render()**：常用
- componentDidUpdate()

​    **3.** **卸载组件:** **由ReactDOM.unmountComponentAtNode()触发**

-  **componentWillUnmount()**：常用
  - 一般在这个钩子中做一些收尾的事情：例如：关闭定时器、取消订阅消息

### 4.3 新生命周期流程图

> 新旧对比：
>
> 1. 废弃三个
> 2. 新提出两个：这两个不咋用

![image-20220316001114310](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220316001114310.png)

**1.** **初始化阶段:** 由ReactDOM.render()触发---初次渲染

1. constructor()
2. **getDerivedStateFromProps** 
3. render()
4. componentDidMount()

  **2.** **更新阶段:** 由组件内部this.setSate()或父组件重新render触发

1. getDerivedStateFromProps
2. shouldComponentUpdate()
3. render()
4. **getSnapshotBeforeUpdate**
5. componentDidUpdate()

  **3.** **卸载组件:** 由ReactDOM.unmountComponentAtNode()触发

componentWillUnmount()

#### 4.6.1 重要的勾子

1. render：初始化渲染或更新渲染调用
2. componentDidMount：开启监听, 发送ajax请求
3. componentWillUnmount：做一些收尾工作, 如: 清理定时器

#### 4.6.2 即将废弃的勾子

- componentWillMount
- componentWillReceiveProps
- componentWillUpdate

现在使用会出现警告，下一个大版本需要加上UNSAFE_前缀才能使用，以后可能会被彻底废弃，不建议使用。

# 5 diff算法

  经典面试题:

- react/vue中的key有什么作用？（key的内部原理是什么？）
- 为什么遍历列表时，key最好不要用index?

​        1. 虚拟DOM中key的作用：

​          1). 简单的说: key是虚拟DOM对象的**标识**, 在**更新**显示时key起着极其重要的作用。

​          2). 详细的说: 当状态中的数据发生变化时，react会根据【新数据】生成【新的虚拟DOM】, 

​                        随后React进行【新虚拟DOM】与【旧虚拟DOM】的diff比较，比较规则如下：

​                  a. 旧虚拟DOM中找到了与新虚拟DOM相同的key：

​                        (1).若虚拟DOM中内容没变, 直接使用之前的真实DOM

​                        (2).若虚拟DOM中内容变了, 则生成新的真实DOM，随后替换掉页面中之前的真实DOM

​                  b. 旧虚拟DOM中未找到与新虚拟DOM相同的key

​                        根据数据创建新的真实DOM，随后渲染到到页面

​      2. 用index作为key可能会引发的问题：

​                1. 若对数据进行：逆序添加、逆序删除等破坏顺序操作:

​                        会产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低。

​                2. 如果结构中还包含输入类的DOM：

​                        会产生错误DOM更新 ==> 界面有问题。

​                3. 注意！如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，

​                  仅用于渲染列表用于展示，使用index作为key是没有问题的。

​      3. 开发中如何选择key?:

​                1.最好使用每条数据的唯一标识作为key, 比如id、手机号、身份证号、学号等唯一值。

​                2.如果确定只是简单的展示数据，用index也是可以的。

 

# 6 脚手架

react提供了一个用于创建react项目的脚手架库：create-react-app

## 创建项目并启动

1.全局安装：npm i -g create-react-app

2.创建项目：create-react-app 项目名

在这一步，有可能会出现：

![image-20220406151355500](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220406151355500.png)

这样可以直接使用：npx create-react-app 项目名

3.等待下载完成，进入项目文件夹，运行一下

比如，我这的项目名称是hello,就先进入hello文件夹

cd hello

npm start //启动这个项目

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220406151408040.png" alt="image-20220406151408040" style="zoom:80%;" />

这个时会自动的打开浏览器，展现这个项目：

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220406151419413.png" alt="image-20220406151419413" style="zoom:80%;" />

## 项目的目录结构

我们先来看一下public这个目录下面的结构：

![image-20220406151430352](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220406151430352.png)

这里面最主要的还是这个Index.html文件：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <!--%PUBLIC_URL%表示public文件夹的路径-->
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <!--用于开启理想视口，用于移动端页面的适配-->
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <!--用于配置浏览器地址栏的颜色（仅支持安卓手机浏览器）-->
    <meta name="theme-color" content="#000000" />
    <!--描述网页信息的-->
    <meta
      name="description"
      content="Web site created using create-react-app"
    />
    <!--用于指定网页添加到手机主屏幕后的图标（仅仅支持ios）-->
    <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
 
    <!--应用加壳时候的配置文件 -->
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
  
    <title>React App</title>
  </head>
  <body>
    <!-- 浏览器不支持JS的运行的时候展现 -->
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
  </body>
</html>
```

src文件：

![image-20220406151444099](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220406151444099.png)

这里面其实最主要的就是App.js以及index.js，一个是组件，一个是将组件渲染到页面中的。

## 第一个脚手架应用

1.我们保持public中的Index.html不变

2.修改src下面的APP.js以及index.js文件

App.js: 【注意：创建好的组件一定要暴露出去】

```jsx
//创建外壳组件APP
import React from 'react'

class App extends React.Component{
    render(){
        return (
            <div>Hello word</div>
        )
    }
}

export default App
```

index.js: 【主要的作用其实就是将App这个组件渲染到页面上】

```jsx
//引入核心库
import React from 'react'
import ReactDOM from 'react-dom'
//引入组件
import App from './App'

ReactDOM.render(<App />,document.getElementById("root"))
```

这样在重新启动应用，就成功了。

我们也不建议这样直接将内容放入App组件中，尽量还是用内部组件。

我们在顶一个Hello组件：

```jsx
import React,{Componet} from 'react'

export default class Hello extends Componet{
    render() {
        return (
            <h1>Hello</h1>
        )
    }
}
```

![image-20220406151526403](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220406151526403.png)

在App组件中，进行使用

```jsx
class App extends Component{
    render(){
        return (
            <div>
                <Hello />
            </div>
        )
    }
}
```

这样的结果和前面是一样的。

但是由于普通的Js和组件都是js，所一最好组件使用jsx去展示。

## 样式冲突

当组件逐渐增多起来的时候，我们发现，组件的样式也是越来越丰富，这样就很有可能产生两个组件中样式名称有可能会冲突，这样会根据引入App这个组件的先后顺序，后面的会覆盖前面的，

为了避免这样的样式冲突，我们采用下面的形式：

1.将css文件名修改： hello.css --- >hello.module.css

2.引入并使用的时候改变方式：

```jsx
import React,{Component}from 'react'
import hello from './hello.module.css'  //引入的时候给一个名称

export default class Hello extends Component{
    render() {
        return (
            <h1 className={hello.title}>Hello</h1>   //通过大括号进行调用
        )
    }
}
```

## 功能界面的组件化编码流程

1.拆分组件:拆分界面，抽取组件

2.实现静态组件

3.实现动态组件

- 动态的显示初始化数据
  - 数据类型
  - 数据名称
  - 保存在哪个组件
- 交互

**注意事项：**

1.拆分组件、实现静态组件。注意className、style的写法

2.动态初始化列表，如何确定将数据放在哪个组件的state中？

- 某个组件使用：放在自身的state中
- 某些组件使用：放在他们共同的父组件中【状态提升】

3.关于父子组件之间的通信

- 父组件给子组件传递数据：通过props传递
- 子组件给父组件传递数据：通过props传递，要求父组件提前给子组件传递一个函数

4.注意defaultChecked 和checked区别，defalutChecked只是在初始化的时候执行一次，checked没有这个限制，但是必须添加onChange方法类似的还有：defaultValue 和value

5.状态在哪里，操作状态的方法就在哪里

## react ajax

React本身只关注与页面，并不包含发送ajax请求的代码，所以一般都是集成第三方的一些库，或者自己进行封装。

推荐使用axios。

在使用的过程中很有可能会出现跨域的问题，这样就应该配置代理。

所谓同源（即指在同一个域）就是两个页面具有相同的协议（protocol），主机（host）和端口号（port）， 当一个请求url的**协议、域名、端口**三者之间任意一个与当前页面url不同即为跨域 。

那么react通过代理解决跨域问题呢

**方法一**

> 在package.json中追加如下配置

```
"proxy":"请求的地址"      "proxy":"http://localhost:5000"  
```

说明：

1. 优点：配置简单，前端请求资源时可以不加任何前缀。
2. 缺点：不能配置多个代理。
3. 工作方式：上述方式配置代理，当请求了3000不存在的资源时，那么该请求会转发给5000 （优先匹配前端资源）

**方法二**

1. 第一步：创建代理配置文件

   ```
   在src下创建配置文件：src/setupProxy.js
   ```

2. 编写setupProxy.js配置具体代理规则：

   ```js
   const proxy = require('http-proxy-middleware')
   
   module.exports = function(app) {
     app.use(
       proxy('/api1', {  //api1是需要转发的请求(所有带有/api1前缀的请求都会转发给5000)
         target: 'http://localhost:5000', //配置转发目标地址(能返回数据的服务器地址)
         changeOrigin: true, //控制服务器接收到的请求头中host字段的值
         /*
         	changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
         	changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:3000
         	changeOrigin默认值为false，但我们一般将changeOrigin值设为true
         */
         pathRewrite: {'^/api1': ''} //去除请求前缀，保证交给后台服务器的是正常请求地址(必须配置)
       }),
       proxy('/api2', { 
         target: 'http://localhost:5001',
         changeOrigin: true,
         pathRewrite: {'^/api2': ''}
       })
     )
   }
   ```

说明：

1. 优点：可以配置多个代理，可以灵活的控制请求是否走代理。
2. 缺点：配置繁琐，前端请求资源时必须加前缀。

## 兄弟之间进行通信

这就要借助消息订阅和发布机制。

举个例子来说就是张三想要跟李四进行通信，张三就需要订阅一个消息【比如A消息】，李四想要给张三数据，就必须发布一个A消息，在发布的同时将数据放入消息中，因为张三订阅了名称为A的消息，此时就能接受到李四发布的消息，从而获取到数据。

这就有点类似于看报纸，甲想要知道每天都发生什么事情，于是订阅了每天日报，乙每天都会发布这个每天日报，因为甲订阅了，于是乙就会每天就给甲方推送，甲方从而获取数据。

**在消息订阅和发布中，我们可以使用PubSubJs进行通信：**

引入PubSubJs:

```jsx
import PubSub from 'pubsub-js'
```

订阅消息：

```jsx
PubSub.subscribe("getSate",(_,data)=>{
            console.log(data)
        })
PubSub.subscribe("订阅的消息名称",回调函数，第一个参数是消息名称，可以使用_来占位，第二个是传递的数据
        })
```

发布消息：

```jsx
PubSub.publish("getSate",{isFrist:false,isLoad:true})
PubSub.publish("订阅的消息名称",传递的数据)
```

## async和await

**async:**

该关键字是放在函数之前的，使得函数成为一个异步函数，他最大的特点就是将函数回封装成Promise，也就是被他修饰的函数的返回值都是Promise对象。而这个Promise对象的状态则是由函数执行的返回值决定的。

如果返回的是一个非promise对象，该函数将返回一个成功的Promise，成功的值则是返回的值；

如果返回的是一个promise对象，则该函数返回的就是该promise对应的状态。

**await**

await右边是一个表达式，如果该表达式返回的是一个Promise对象，则左边接收的结果就是该Promise对象成功的结果，如果该Promise对象失败了，就必须使用try..catch来捕获。如果该表达式返回的是是一个不是promise对象，则左边接受的就是该表达式的返回值。

当 [await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await) 关键字与异步函数一起使用时，它的真正优势就变得明显了 —— 事实上， **await 只在异步函数里面才起作用**。它可以放在任何异步的，基于 promise 的函数之前。它会暂停代码在该行上，直到 promise 完成，然后返回结果值。在暂停的同时，其他正在等待执行的代码就有机会执行了。

举个例子：

```js
 f1 = () =>{
        return new Promise((resolve,reject)=>{
            // resolve(1);
            reject("错误")
        })
    }

    async function test(){
        try{
           const p =  await f1();
           console.log(p)
        }catch(error){
            console.error(error)
        }
    }
    test();
```

## fetch

以前发送请求，使用ajax或者axios，现在还可以使用fetch。这个是window自带的，和xhr是一个级别的。

可以查看这个文章，写的真的不错：

[fetch](http://www.ruanyifeng.com/blog/2020/12/fetch-tutorial.html)

# 7 React 路由

## SPA

单页Web应用(single page web application，SPA)。整个应用只有一个完整的页面。

点击页面中的链接**不会刷新页面**，**只会做页面的局部更新**。

数据都需要通过ajax请求获取,并在前端异步展现

单页面 多组件

