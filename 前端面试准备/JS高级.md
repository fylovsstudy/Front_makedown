## 一 基础总结深入

### 1 数据类型

#### 1.1  数据类型的分类

JS中一共有6中数据类型，前五种是基本数据类型，Object是引用，对象数据类型。

- 基本类型：

  - String 字符串
    - js中字符串需要用引号引起来，使用单双引号都可以
    - \转义:\n换行  \t指标符
  
  
    - Number 数值：JS中所有数值都是Number类型，包括整数和浮点数
  
    - Boolean 布尔值：true/false
  
    - NULL 空值：null
  
    - Undefined 未定义:undefined
  


- 对象类型
  - object：任意对象都是object类型
  - Function：一种特别的对象，特别在可以执行
  - Array：一种特别的对象（数值下表，内部数据是有序的）

#### 1.2 数据类型判断

- typeof 
  - 返回的是数据类型的字符串表达
  - 可以判断undefined/数值/字符串/布尔值/function
  - 不能区分null和object  array和object 
- instanceof：判断对象的具体类型
- ===（不会做数据转换，判断两个数据是否完全相等）
  - 可以判断undefined/null

```javascript
var a
console.log(a,typeof(a)，typeof a ==='undefined',a===undefined)//undfined "undefined" true true
console.log(undefined==='undefined')//false
//typeof返回的是数据类型的字符串表达

a=3
console.log(typeof a==='number')//true
a='sadsad'
console.log(typeof a==='string')//true
a=true
console.log(typeof a==='boolean')//true
a=null
console.log(typeof a)//'object'？？？？？？？？？
console.log(a===null)//true
```

```js
//instanceof 用于判断对象的类型
var b1={
    b2:[1,'abc',console.log],
    b3:function(){
        console.log('b3')
        return function(){
            return 'sadalkjbvs'
        }
    }
}
console.log(b1 instanceof Object，b1 instanceof array)//A是不是B的实例 true false
console.log(b1.b2 instanceof Array,b1.b2 instanceof Object)//true true
//Object()是一个构造函数
console.log(b1.b2.b3 instanceof Function,b1.b2 instanceof Object)//true true 函数也是对象
console.log(typeof b1.b3==='funciton')//true
console.log(typeof b1.b2[2]==='funciton')//true
b1.b2[2](4)//4
console.log(b1.b3()())//'sadalkjbvs'
```

1. undefined和null的区别

   undefined 是定义了未赋值

   null是定义了也赋值了但是值为null

   ```
   var a;
   console.log(a)//undefined
   a = null
   console.log(a)//null
   ```

2. 什么时候给变量赋值为null

​	初始赋值，表明将要赋值为对象

​	结束前，让对象成为垃圾对象（被垃圾回收器回收）

3. 严格区分变量类型和数据类型
   - 数据的类型
     - 基本类型
     - 对象类型
   - 变量类型（变量内存值的类型）
     - 基本类型：保存的就是基本类型的数据
     - 引用类型：保存的是地址值

```
var a=2
```

### 2 回调函数

**什么函数才是回调函数**

1. 你定义的
2. 你没有调
3. 但最终它执行了

**常见的回调函数**

1. dom事件回调函数
2. 定时器回调函数
3. ajax请求回调函数
4. 生命周期回调函数

```js
// dom事件回调函数
document.getElementById('btn').onclick = function () {
    alert(this.innerHTML);
}
// 定时器  
// 超时定时器
// 循环定时器
setTimeout(function () {//定时器回调函数
    alert("到点了");
}, 2000)
```

### 3 IIFE

1. 全称: `Immediately-Invoked Function Expression` 自调用函数
2. 作用:
   - 隐藏实现
   - 不会污染外部(一般指全局)命名空间
   - 用它来编码js模块
3. 代码示例

```js
  (function () { //匿名函数自调用
    var a = 3
    console.log(a + 3)
  })()
  console.log(a) // a is not defined
  
  //此处前方为何要一个`;`-->因为自调用函数外部有一个()包裹,可能与前方以()结尾的代码被一起认为是函数调用
  //不加分号可能会被认为这样 console.log(a)(IIFE)
  ;(function () {//不会污染外部(全局)命名空间-->举例
    let a = 1;
    function test () { console.log(++a) } //声明一个局部函数test
    window.$ = function () {  return {test: test} }// 向外暴露一个全局函数
  })()
 test ()  //test is not defined
  $().test() // 1. $是一个函数 2. $执行后返回的是一个对象
```

### 4 this

1. this 是什么

   - 任何函数本质上都是通过某个对象来调用的，如果没有直接指定就是window

   - 所有函数内部都有一个变量this

   - 它的值是调用函数的当前对象

2. 如何确定this 的值

   - test() ：window
   - p.test(): p
   - new test():新创建的对象
   - p.call(obj):  obj

## 二 函数高级

### 2.1 原型与原型链

#### 2.1.1 原型 [prototype]

1. 函数的`prototype`属性

- 每个函数都有一个prototype属性, 它默认指向一个Object空的实例对象(即称为: 原型对象)
- 原型对象中有一个属性constructor, 它指向函数对象

2. 给原型对象添加属性(`一般都是方法`)

- 作用: 函数的所有实例对象自动拥有原型中的属性(方法)

```js
// 每个函数都有一个prototype属性, 它默认指向一个Object空对象(即称为: 原型对象)
console.log(Date.prototype, typeof Date.prototype)
function Fun () { }
console.log(Fun.prototype)  // 默认指向一个Object空对象(没有我们的属性)

// 原型对象中有一个属性constructor, 它指向函数对象
console.log(Date.prototype.constructor===Date)
console.log(Fun.prototype.constructor===Fun)

//给原型对象添加属性(一般是方法) ===>实例对象可以访问
Fun.prototype.test = function () { console.log('test()') }
var fun = new Fun()
fun.test()
```

#### 2.1.2 显式原型与隐式原型

```js
//定义构造函数
  function Fn() {
   // 内部默认执行语句: this.prototype = {}
    }
  // 1. 每个函数function都有一个prototype，即显式原型属性, 默认指向一个空的Object对象
  console.log(Fn.prototype)
  // 2. 每个实例对象都有一个__proto__，可称为隐式原型
  //创建实例对象                       
  var fn = new Fn()  // 内部默认执行语句: this.__proto__ = Fn.prototype
  console.log(fn.__proto__)
  // 3. 对象的隐式原型的值为其对应构造函数的显式原型的值
  console.log(Fn.prototype===fn.__proto__) // true
  //给原型添加方法
  Fn.prototype.test = function () {
    console.log('test()')
  }
  //通过实例调用原型的方法
  fn.test()
```

1. 每个函数function都有一个`prototype`，即`显式`原型(属性)
2. 每个实例对象都有一个[`__ proto __`]，可称为`隐式`原型(属性)
3. 对象的隐式原型的值为其对应构造函数的显式原型的值
4. 内存结构

![image-20220223205834139](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220223205834139.png)

![image-20220224000245496](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220224000245496.png)

5. 总结:

- 函数的[`prototype`]属性: 在定义函数时自动添加的, 默认值是一个空Object对象
- 对象的[`__ proto __`]属性: 创建对象时自动添加的, `默认值为构造函数的prototype属性值`
- 程序员能直接操作显式原型, 但不能直接操作隐式原型(ES6之前)

6. 不好理解的点：

- 函数的显式原型执行的对象默认是空的Object实例对象（但Object不满足）

  ```js
  console.log(Fn.prototype instanceof Object)//true
  console.log(Object.prototype instanceof Object)//false
  console.log(Function.prototype instanceof Object)//true
  ```

- 所有函数都是Function的实例，包括他本身。Function 是它自身的实例

```js
console.log(Function.__proto__ === Function.prototype)//true
```

- Object的原型对象是原型链的尽头

```js
Object.prototype.__proto__ = null
```

7. 代码示例

   ```js
   //定义构造函数
     function Fn() {
      // 内部默认执行语句: this.prototype = {}
       }
     // 1. 每个函数function都有一个prototype，即显式原型属性, 默认指向一个空的Object对象
     console.log(Fn.prototype)
     // 2. 每个实例对象都有一个__proto__，可称为隐式原型
     //创建实例对象
     var fn = new Fn()  // 内部默认执行语句: this.__proto__ = Fn.prototype
     console.log(fn.__proto__)
     // 3. 对象的隐式原型的值为其对应构造函数的显式原型的值
     console.log(Fn.prototype===fn.__proto__) // true
     //给原型添加方法
     Fn.prototype.test = function () {
       console.log('test()')
     }
     //通过实例调用原型的方法
     fn.test()
   ```

#### 2.1.3 原型链

##### ①原型链

 - 访问一个对象的属性时，
  - 先在自身属性中查找，找到返回
   - 如果没有, 再沿着[`__ proto __`]这条链向上查找, 找到返回
  - 如果最终没找到, 返回undefined
   
   - 别名: 隐式原型链
   - 作用: 查找对象的属性(方法)

##### ②构造函数/原型/实例对象的关系(图解)


 ps:所有函数的[`__ proto __`]都是一样的

##### ③ 属性问题

 - 读取对象的属性值时: 会自动到原型链中查找
 - 设置对象的属性值时: 不会查找原型链, 如果当前对象中没有此属性, 直接添加此属性并设置其值
 - 方法一般定义在原型中, 属性一般通过构造函数定义在对象本身上
 - 代码示例

 ```js
   function Fn() { }
   Fn.prototype.a = 'xxx'
   var fn1 = new Fn()
   console.log(fn1.a, fn1) //xxx Fn{}
 
   var fn2 = new Fn()
   fn2.a = 'yyy'
   console.log(fn1.a, fn2.a, fn2) //xxx yyy  Fn{a: "yyy"}
 
   function Person(name, age) {
     this.name = name
     this.age = age
   }
 //属性在构造函数里面
 //方法在原型链上
   Person.prototype.setName = function (name) {
     this.name = name
   }
   var p1 = new Person('Tom', 12)
   p1.setName('Bob')
   console.log(p1)  //Person {name: "Bob", age: 12}
 
   var p2 = new Person('Jack', 12)
   p2.setName('Cat')
   console.log(p2) //Person {name: "Cat", age: 12}
   console.log(p1.__proto__===p2.__proto__) // true   -->所以方法一般定义在原型中
 ```

![image-20220224234911168](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220224234911168.png)

#### 2.1.4 instanceof

1. instanceof是如何判断的?

- 表达式: A instanceof B
- 如果B函数的显式原型对象在A对象的原型链上, 返回true, 否则返回false

2. Function是通过new自己产生的实例

```js
/*案例1*/
 function Foo() {  }
 var f1 = new Foo()
 console.log(f1 instanceof Foo) // true
 console.log(f1 instanceof Object) // true

 /*案例2*/
 console.log(Object instanceof Function) // true
 console.log(Object instanceof Object) // true
 console.log(Function instanceof Function) // true
 console.log(Function instanceof Object) // true

 function Foo() {}
 console.log(Object instanceof  Foo) // false
```

#### 2.1.5 面试题

```js
 /*
 测试题1
  */
 function A () {}
 A.prototype.n = 1
 let b = new A()
 A.prototype = { n: 2, m: 3}
 let c = new A()
 console.log(b.n, b.m, c.n, c.m) // 1 undefined 2 3
```

**题解**

![image-20220226153501462](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220226153501462.png)

```js
 /*
  测试题2
  */
 function F (){}
 Object.prototype.a = function(){
   console.log('a()')
 }
 Function.prototype.b = function(){
   console.log('b()')
 }
 
   
 f.a() //a()
 f.b() //f.b is not a function -->找不到
 F.a() //a()
 F.b() //b()

 console.log(f)
 console.log(Object.prototype)
 console.log(Function.prototype)
```

![image-20220226160808136](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220226160808136.png)

### 2.2 执行上下文与执行上下文栈

#### 2.2.1 变量提升和函数声明

1. 变量声明提升

- 通过var定义(声明)的变量, 在定义语句之前就可以访问到
- 值: undefined

2. 函数声明提升

- 通过function声明的函数, 在之前就可以直接调用
- 值: 函数定义(对象)

3. 引出一个问题: 变量提升和函数提升是如何产生的?

```js
/*
 面试题 : 输出 undefined
  */
 var a = 3
 function fn () {
   console.log(a)
   var a = 4 //变量提升
 }
 fn()  //undefined
'--------------------------------------------'
 console.log(b) //undefined  变量提升
 fn2() //可调用  函数提升
 // fn3() //不能  变量提升
 var b = 3
 function fn2() {  console.log('fn2()') }
 var fn3 = function () { console.log('fn3()') }
```

#### 2.2.2 执行上下文

1. 代码分类(位置)

- 全局代码
- 函数(局部)代码

2. 全局执行上下文

- 在执行全局代码前将window确定为全局执行上下文
- 对全局数据进行预处理
  - var定义的全局变量==>undefined, 添加为window的属性
  - function声明的全局函数==>赋值(fun), 添加为window的方法
  - this==>赋值(window)
- 开始执行全局代码

3. 函数执行上下文

- 在调用函数, 准备执行函数体之前, 创建对应的函数执行上下文对象(虚拟的, 存在于栈中)
- 对局部数据进行预处理
  - 形参变量==>赋值(实参)==>添加为执行上下文的属性
  - `arguments`==>赋值(实参列表), 添加为执行上下文的属性 -->[不懂的同学看这里](https://gitee.com/link?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2Forphaned%2FWeb%2FJavaScript%2FReference%2FFunctions%2Farguments)
  - var定义的局部变量==>undefined, 添加为执行上下文的属性
  - function声明的函数 ==>赋值(fun), 添加为执行上下文的方法
  - this==>赋值(调用函数的对象)
- 开始执行函数体代码

#### 2.2.3 执行上下文栈

**函数执行上下文只有再函数调用的时候才会产生！**

1. 在全局代码执行前, JS引擎就会创建一个栈（先进后出）来存储管理所有的执行上下文对象
2. 在全局执行上下文(window)确定后, 将其添加到栈中(压栈)-->`所以栈底百分百是[window]`
3. 在函数执行上下文创建后, 将其添加到栈中(压栈)
4. 在当前函数执行完后,将栈顶的对象移除(出栈)
5. 当所有的代码执行完后, 栈中只剩下window
6. `上下文栈数==函数调用数+1`
6. 函数提升优先级高于变量提升,且不会被变量声明覆盖,但是会被变量赋值覆盖

```js
//1. 进入全局执行上下文
var a = 10
var bar = function (x) {
  var b = 5
  foo(x + b)   //3. 进入foo执行上下文           
}
var foo = function (y) {
  var c = 5
  console.log(a + c + y)
}
bar(10) //2. 进入bar函数执行上下文
```

![image-20220227200119798](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220227200119798.png)

#### 2.2.4 面试题

函数提升优先级高于变量提升,且不会被变量声明覆盖,但是会被变量赋值覆盖

```js
*/
function a() {}
var a
console.log(typeof a) // 'function'
//函数提升优先级高于变量提升,且不会被变量声明覆盖,但是会被变量赋值覆盖

/*
测试题2:
*/
if (!(b in window)) {
 var b = 1
}
console.log(b) // undefined

/*
测试题3:
*/
var c = 1
function c(c) {
 console.log(c)
 var c = 3 //与此行无关
}
c(2) // 报错  c is not a function
```

### 2.3 作用域和作用域链

#### 2.3.1 作用域

1. 理解

- 就是一块"地盘", 一个代码段所在的区域
- 它是静态的(相对于上下文对象), 在编写代码时就确定了

2. 分类

- 全局作用域
- 函数作用域
- 没有块作用域(ES6有了) -->(java语言也有)

3. 作用

- 隔离变量，不同作用域下同名变量不会有冲突

4. 作用域数量

   n+1 ， n：函数定义的个数

```js
/*  //没块作用域
 if(true) { var c = 3 }
 console.log(c)
 */
 var 	a = 10,
   		b = 20
 function fn(x) {
   var a = 100, c = 300;
   console.log('fn()', a, b, c, x) //100 20 300 10
     // 现在里面找  没有的话就去外面找
   function bar(x) {
     var a = 1000, d = 400
     console.log('bar()', a, b, c, d, x)
   }
   bar(100)//1000 20 300 400 100
   bar(200)//1000 20 300 400 200
 }
 fn(10)
```

![image-20220227211447617](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220227211447617.png)

#### 2.3.2 作用域和执行上下文的区别

1. 区别1

- 全局作用域之外，每个函数都会创建自己的作用域，作用域再函数定义的时候就已经确当了，而不是再函数调用的时候确定的
- 全局上下文是在全局作用域确定之后，js代码马上执行之前创建
- 函数执行上下文环境是在调用函数时，函数体代码执行之前创建

2. 区别2

- 作用域是静态的, 只要函数定义好了就一直存在, 且不会再变化
- 执行上下文是动态的, 调用函数时创建, 函数调用结束时就会自动释放

3. 联系
   1. 执行上下文(对象)是从属于所在的作用域
   2. 全局上下文环境==>全局作用域
   3. 函数上下文环境==>对应的函数使用域

#### 2.3.3作用域链

1. 理解

- 多个上下级关系的作用域形成的链, 它的方向是从下向上的(从内到外)
- 查找变量时就是沿着作用域链来查找的

![image-20220227212113276](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220227212113276.png)

2. 查找一个变量的查找规则

- 在当前作用域下的执行上下文中查找对应的属性, 如果有直接返回, 否则进入2
- 在上一级作用域的执行上下文中查找对应的属性, 如果有直接返回, 否则进入3
- 再次执行2的相同操作, 直到全局作用域, 如果还找不到就抛出找不到的异常

```js
var a = 1
 function fn1() {
   var b = 2
   function fn2() {
     var c = 3
     console.log(c)
     console.log(b)
     console.log(a)
     console.log(d)
   }
   fn2()
 }
 fn1()
```

#### 2.3.4 相关面试题

```js
var x = 10;
function fn() { console.log(x); }
function show(f) {
    var x = 20;
    f();
}
show(fn); //输出10
//作用域是静态的  在函数定义的时候就确定了 不会因为函数的调用改变
```

![image-20220227212835332](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220227212835332.png)

```js
var fn = function () {
 console.log(fn)
}
fn()

var obj = { //对象变量不能产生局部作用域,所以会找到全局去,导致报错
 fn2: function () {
  console.log(fn2)
  //console.log(this.fn2)
 }
}
obj.fn2()
```

### 2.4 闭包

1. 如何产生闭包？

​	当一个嵌套的内部（子）函数引用了嵌套的外部（父）函数的变量（函数）时，就产生了闭包

2. 闭包到底是什么？

- 可以通过chrome 工具 ，debug的方式查看
- 理解一：闭包是嵌套的内部函数

- 理解二：包含被引用变量（函数）的对象

3. 产生闭包的条件？

- 函数嵌套
- 内部函数引用了外部函数的数据
- 执行外部函数，不一定要调用内部函数，内部函数只要有定义就可以了

```js
function fn1() {
    var a = 2
    var b = 'abc'
    function fn2() {  //执行函数定义就会产生闭包，不用调用内部函数
        console.log(a)
    }
}
fn1()
```

4. 常见的闭包

- 将函数作为一个函数的返回值
- 将函数作为实参传递给另一个函数调用

```js
//1. 将函数作为一个函数的返回值
function fn1() {
    //此时闭包已经产生（函数提升，内部函数对象已经创建了）
    var a = 2
    function fn2() {
        a++
        console.log(a)
}
    return fn2
}
//看产生了几个闭包，就是看外部函数调用了几次：
var f = fn1()//调用了一次外部函数
f()//3  调用的是内部函数
f()//4 调用的是内部函数
f = null//闭包死亡（包含闭包的函数对象成为垃圾对象）

//2. 将函数作为实参传递给另一个函数调用
function showDelay(msg,time){
    setTimeout(function() {
        alert(msg)
    },time)
}
showDelay ('aa',200)
```

5. 闭包的作用

   1. **使函数内部的变量在函数执行完后，仍然存活在内存中（延长了局部变量的声明周期）**
   2. **让函数外部可以操作（读写）到函数内部的数据（变量/函数）**

6. 问题

   1. 函数执行完后，函数内部声明的局部变量是否还存在？

      - 一般情况下不存在

      - 只有存在于闭包中的局部变量存在，在闭包里面。在上面的例子里面。fn1执行完以后，a还存在于闭包里面。而fn2和fn3都释放了，因为没有被内部函数引用。但是fn3对应的函数对象还存在，因为被f引用了。
      - 如果把 var f = fn3() 修改为fn3() ，则闭包就不存在了。因为这个时候就没有引用指向，内部函数就称为垃圾对象了。

   2. 在函数外部能直接访问函数内部的局部变量吗？

      不能。但是我们可以通过闭包让外部操作它

7. 闭包的产生和死亡
   1. 产生：在嵌套函数内部定义执行完成时就产生了（不是调用）
   2. 死亡：在嵌套的内部函数成为垃圾对象时

8. 闭包的应用2：定义JS模块

- 具有特定功能的js文件
- 将所有的数据和功能都分装在一个函数内部（私有的）
- 只向外暴露一个包含n个方法的对象或函数
- 模块的使用者，只需要通过模块暴露的对象调用方法来实现对应的功能

```js
//js方法一 这种好一点
(function () {
    var msg = 'my atguigu'
    function doSomething() {
        console.log('doSOmething() ' + msg.toUpperCase())
    }
    function doOtherthing() {
        console.log('doSOmething() ' + msg.toLowerCase())
    }
    window.myModule2 = {
        doSomething: doSomething,
        doOtherthing: doOtherthing
    }
})()
// 立即执行函数
//html
myModule2.doSomething()
myModule2.doOtherthing()

//js 方法二
function myModule() {
    var msg = 'my atguigu'
    function doSomething() {
        console.log('doSOmething() ' + msg.toUpperCase())
    }
    function doOtherthing() {
        console.log('doSOmething() ' + msg.toLowerCase())
    }
    return {
        doSomething: doSomething,
        doOtherthing: doOtherthing
    }
}
//html
var my = myModule()
my.doSomething()
my.doOtherthing()
```

9. 闭包的缺点：

- 函数执行完后，函数内的局部变量没有释放，占用内存额事件会变长
- 容易造成内存泄漏

- 解决：
  - 能不用闭包就不用
  - 及时释放

```js
function fn1() {
    var arr = new Array[100000]
    function fn2() {
        console.log(arr.length)
    }
    return fn2
}
var f = fn1()
f()
f = null //让内部函数成为垃圾对象 --> 回收闭包
```

10. 内存溢出和内存泄漏

- 内存溢出

  - 一种程序运行出现的错误

  - 当程序运行需要的内存超过了运行的内存时，就会抛出内存溢出的错误

- 内存泄露

  - 占用的内存没有及时释放

  - 内存泄漏累计多了就容易导致内存溢出

  - 常见的内存泄露

    - 意外的全局变量

    - 没有及时清理的计时器或回调函数

      ```js
      var intervalID = serInterval(function() {
          console.log("lllal")
      },2000)
      
      //clearInterval(intervalId)
      ```

    - 闭包

11. 面试题

```js
var name = "The Window"
var object = {
    name: "My Object",
    getNameFunc: function () {
        console.log(this)
        return function () {
            return this.name
            console.log(this)
        }
    }
}
alert(object.getNameFunc()()) //The Window 直接执行函数去了  没有通过object，只是通过object调用了getNameFunc

var name2 = "The Window"
var object2 = {
    name: "My Object",
    getNameFunc: function () {
        var that = this
        return function () {
            return that.name
            // 有闭包
        }
    }
}
alert(object2.getNameFunc()()) //My Object
```

## 三 面向对象高级

### 3.1 对象创建模式

方式一： Object 构造函数模式

套路：先创建空的Object 对象，在动态添加属性/方法

使用场景：起始时不确定对象内部数据

问题：语句太多

```js
 var p = new Object()
    p.name = 'Tom'
    p.age = 12
    p.setname = function (name) {
        this.name = name
    }
```

方式二：对象字面量模式

套路：使用{} 创建对象，同时指定属性和方法

使用场景：起始对象内部数据时确定的

问题：如果创建多个对象有重复代码

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220302195721536.png" alt="image-20220302195721536" style="zoom:67%;" />

方式三：工厂模式

套路：通过工厂函数动态创建对象并返回

使用场景：需要创建多个对象

问题：对象没有一个具体的类型，都是Object类型

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220302200231054.png" alt="image-20220302200231054" style="zoom:67%;" />

方式四：自定义构造函数模式

套路：自定义构造函数，通过new创建对象

使用场景：需要创建多个类型确定的对象

问题：每个对象都有相同的数据，浪费内存

方式五：自定义构造函数＋原型的组合模式

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220302201658449.png" alt="image-20220302201658449" style="zoom:67%;" />

### 3.2 继承模式

方式一：原型链继承

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220302212705288.png" alt="image-20220302212705288" style="zoom:67%;" />

套路： 

 	1. 定义父类型构造函数
 	2. 给父类型的原型添加方法
 	3. 定义子类型的构造函数
 	4. 创建父类型的对象赋值给子类型的原型
 	5. 将子类型原型的构造属性设置为子类型
 	6. 给子类型原型添加方法
 	7. 创建子类型的对象：可以调用父类型的方法

关键：

​	子类型的原型是父类型的一个实例对象

```js
//子类型的原型是父类型的原型对象
Sub.prototype = new Supper()
```

方式二：借用构造函数继承

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220302212619074.png" alt="image-20220302212619074" style="zoom:67%;" />

**方式三：组合继承**

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220302212428503.png" alt="image-20220302212428503" style="zoom:67%;" />

## 四 线程机制与事件机制

### 1 进程与线程

#### 4.1.1 进程和线程

![image-20210728115630974](https://gitee.com/hongjilin/hongs-study-notes/raw/master/%E7%BC%96%E7%A8%8B_%E5%89%8D%E7%AB%AF%E5%BC%80%E5%8F%91%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/HTML+CSS+JS%E5%9F%BA%E7%A1%80%E7%AC%94%E8%AE%B0/JavaScript%E7%AC%94%E8%AE%B0/A_JavaScript%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%E4%B8%AD%E7%9A%84%E5%9B%BE%E7%89%87/image-20210728115630974.png)

#### 4.1.2 进程

1. 程序的一次执行,它`占有一片独有的内存空间`
2. 可以通过windows任务管理器查看进程
3. 多进程运行: 一应用程序可以同时启动多个实例运行

- 可以看出每个程序的内存空间是相互独立的

![image-20220303135323864](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220303135323864.png)

#### 4.1.3 线程

- 是进程内一个独立的执行单元
- 是程序执行的一个完整流程
- 是CPU的最小调度单元

#### 4.1.4 进程和线程

- 应用程序必须运行在某个进程的某个线程上
- 一个进程中至少有一个运行的线程：主线程，进程启动后自动创建
- 一个进程内的数据可以供其中的多个线程直接共享
- 多个进程之间的数据是不能直接共享的
- 线程池(thread pool) ：保存多个线程对象的容器，实现线程对象的反复利用
- 比较单线程与多线程?
  - 多线程:
    - 优点:能有效提升CPU的利用率
    - 缺点
    - 创建多线程开销
    - 线程间切换开销
    - 死锁与状态同步问题
  - 单线程:
    - 优点:顺序编程简单易懂
    - 缺点:效率低

#### 4.1.5 JS是单线程还是多线程?

JS是单线程运行的 , 但使用H5中的 Web Workers可以多线程运行

- 只能由一个线程去操作DOM界面
- 具体原因可看下方[3、JS是单线程的](https://gitee.com/hongjilin/hongs-study-notes/blob/master/编程_前端开发学习笔记/HTML+CSS+JS基础笔记/JavaScript笔记/A_JavaScript进阶学习笔记.md#3、JS是单线程的)部分给出的详解

#### 浏览器运行是单线程还是多线程?

都是多线程运行的

#### 浏览器运行是单进程还是多进程?

有的是单进程:

- firefox
- 老版IE

有的是多进程:

- chrome
- 新版IE

如何查看浏览器是否是多进程运行的呢? 任务管理器-->进程

### 2 浏览器内核

支撑浏览器运行的最核心的程序

#### 4.2.1 不同浏览器的内核

- Chrome, Safari : webkit
- firefox : Gecko
- IE : Trident
- 360,搜狗等国内浏览器: Trident + webkit

#### 4.2.2 内核是由什么模块组成

主线程

1. js引擎模块 : 负责js程序的编译与运行
2. html,css文档解析模块 : 负责页面文本的解析(拆解)
3. dom/css模块 : 负责dom/css在内存中的相关处理
4. 布局和渲染模块 : 负责页面的布局和效果的绘制
5. 布局和渲染模块 : 负责页面的布局和效果的绘制

分线程

- 定时器模块 : 负责定时器的管理
- 网络请求模块 : 负责服务器请求(常规/Ajax)
- 事件响应模块 : 负责事件的管理

