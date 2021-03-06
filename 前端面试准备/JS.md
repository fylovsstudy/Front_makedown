## 1 JS认知

- ECMAscript是JS的标准
- JS包括：ES，DOM，BOM
- JS是解释性语言，是动态语言，基于原型的面向对象。

```javascript
//输出语句
//alert() 警告框
//document.write("");向body中输出一个内容
//console.log("");向控制台输出一个内容
```

JS编写位置：

```js
<button onclick="alert('')">点我一下</button>
<a herf="javascript:alert('点')">让你点我一下</a>
//虽然可以写在标签属性中，但是他们属于结构和行为耦合，不方便维护
//可以将js代码编写到script标签中
//可以写到外部文件中，可以在不同页面中同时引用，也可以利用到浏览器的缓存机制
<script type="text/javascript" src="js/script.js"></script>
```

JS严格区分大小写，以分号结束，如果不写分号，浏览器回自动增加，但是回消耗一些系统资源，有时浏览器会加错分号，所以必须写。JS中忽略空格和换行，可以利用这个特点进行格式化。

#### 1.1 字面量和变量

- 都是不可改变的值 比如：1，2，3，4，5
- 字面量可以直接使用但是一般不会直接使用字面量
- 变量：可以用来保存字面量，而且可以任意改变，所以用变量去保存字面量。
- 变量使用：声明变量；赋值变量

```js
var a = 55;
```

#### 1.2 标识符

- 标识符中可以含有字母数字_$
- js底层保存标识符实际上是采用Unicode编码，所以理论上讲，所有的utf-8中含有的内容都可以作为标识符。

## 2 数据类型

#### 六种数据类型

JS中一共有6中数据类型，前五种是基本数据类型，Object是引用数据类型。

- String 字符串
  - js中字符串需要用引号引起来，使用单双引号都可以
  - \转义:\n换行  \t指标符

- Number 数值：JS中所有数值都是NUmber类型，包括整数和浮点数
- Boolean 布尔值
- NULL 空值
- Undefined 未定义
- Object 对象

#### 1.String 字符串

JS中的字符串需要使用引号引起来双引号或单引号都行
在字符串中使用\作为转义字符

```js
\'  ==> '  
\"  ==> "  
\n  ==> 换行  
\t  ==> 制表符  
\\  ==> \
```

使用typeof运算符检查字符串时，会返回”string”

#### 2.Number 数值

**JS中所有的整数和浮点数都是Number类型**

最大能表示的值：Number.MAX_VALUE= 1.7976931348623157e+308

特殊的数字：能赋值给变量
Infinity 正无穷 a = Infinity ,能赋值
-Infinity 负无穷
NaN 非法数字（Not A Number）
其他进制的数字的表示：
0b 开头表示二进制，但是不是所有的浏览器都支持
0 开头表示八进制
0x 开头表示十六进制

使用typeof检查一个Number类型的数据时，会返回”number”
（包括NaN 和 Infinity）

#### 3.Boolean 布尔值

布尔值主要用来进行逻辑判断，布尔值只有两个
true 逻辑的真
false 逻辑的假
使用typeof检查一个布尔值时，会返回”boolean”

#### 4.Null 空值

空值专门用来表示为**空的对象**，Null类型的值只有一个
null
**使用typeof检查一个Null类型的值时会返回”object”**

#### 5.Undefined 未定义

**如果声明一个变量但是没有为变量赋值此时变量的值就是undefined**
该类型的值只有一个 undefined
使用typeof检查一个Undefined类型的值时，会返回”undefined”

#### 引用数据类型

Object 对象

## 3 类型转换

类型转换就是指将其他的数据类型，转换为String Number 或 Boolean

### 转换为String

#### 方式一（强制类型转换）：

**调用被转换数据的toString()方法**

例子：

```js
var a = 123;
console.log(typeof a);//number
a = a.toString();
console.log(typeof a);//string
var a = null;
a.toString();//错！
```

注意：

**该方法不会影响到原变量，它会将转换的结果返回。这个方法不适用于null和undefined**
由于这两个类型的数据中没有方法，所以调用toString()时会报错

#### 方式二（强制类型转换）：

**调用String()函数**
例子：

```js
var a = 123;  
a = String(a);
```

原理：**对于Number Boolean String实际上都会调用他们的toString()方法来将其转换为字符串。对于null值和undefined不会调用toString()方法。对于null值，直接转换为字符串”null”。对于undefined直接转换为字符串”undefined”**

#### 方式三（隐式的类型转换）:

**为任意的数据类型 +””**
例子：

```js
var a = true;  
a = a + "";
```

原理：和String()函数一样

### 转换为Number

#### 方式一（强制类型转换）：

**调用Number()函数**
例子：

```js
var s = "123";  
s = Number(s);
```

1. 字符串 > 数字
   如果字符串是一个合法的数字，则直接转换为对应的数字
   如果字符串是一个非法的数字，则转换为NaN
   如果是一个空串或纯空格的字符串，则转换为0
2. 布尔值 > 数字
   true转换为1
   false转换为0
3. 空值 > 数字
   null转换为0
4. 未定义 > 数字
   undefined 转换为NaN

#### 方式二（强制类型转换）：

调用parseInt()或parseFloat()
这两个函数专门用来将一个字符串转换为数字的

如果对非String使用parseInt()或parseFloat()，它会**先将其转换为String**然后在操作 parseInt()
可以将**一个字符串中的有效的整数位**提取出来，并转换为Number
例子：

```js
var a = "123.456px";  
a = parseInt(a); //123
```

如果需要可以在parseInt()中指定一个第二个参数，来指定进制parseFloat()可以将一个**字符串中的有效的小数位**提取出来，并转换为Number
例子：

```js
var a = "123.456px";  
a = parseFloat(a); //123.456
```

#### 方式三（隐式的类型转换）：

使用一元的+来进行隐式的类型转换
例子：

```js
var a = "123";  
a = +a;
```

**原理：和Number()函数一样**

### 转换为布尔值

#### 方式一（强制类型转换）：

使用Boolean()函数
例子：

```js
var s = "false";  
s = Boolean(s); //true
```

转换的情况
字符串 > 布尔
除了空串其余全是true

数值 > 布尔
除了0和NaN其余的全是true

null、undefined > 布尔
都是false

对象 > 布尔
都是true

#### 方式二（隐式类型转换）：

**为任意的数据类型做两次非运算，即可将其转换为布尔值**
例子：

```js
var a = "hello";  
a = !!a; //true
```

## 4 基础语法

### 运算符

运算符也称为操作符
通过运算符可以对一个或多个值进行运算或操作

#### typeof运算符

用来检查一个变量的数据类型
语法：typeof 变量
它会返回一个用于描述类型的**字符串**作为结果

#### 算数运算符

+对两个值进行加法运算并返回结果

-对两个值进行减法运算并返回结果

*对两个值进行乘法运算并返回结果

/对两个值进行除法运算并返回结果

%对两个值进行取余运算并返回结果

**除了加法以外，对非Number类型的值进行运算时，都会先转换为Number然后在做运算。**
而做加法运算时，如果是两个字符串进行相加，则会做拼串操作，将两个字符连接为一个字符串。
任何值和字符串做加法，都会先转换为字符串，然后再拼串

#### 一元运算符

一元运算符只需要一个操作数

##### 一元的+

就是正号，不会对值产生任何影响，但是可以将一个非数字转换为数字
例子：

```js
var a = true;  
a = +a;
```

##### 一元的-

就是负号，可以对一个数字进行符号位取反
例子：

```js
var a = 10;  
a = -a;//-10
```

##### 自增

自增可以使变量在原值的基础上自增1
自增使用 ++
自增可以使用 前++（++a）后++(a++)
无论是++a 还是 a++都会立即使原变量自增1
不同的是++a和a++的值是不同的，
++a的值是变量的新值（自增后的值）
a++的值是变量的原值（自增前的值）

##### 自减

自减可以使变量在原值的基础上自减1
自减使用
自减可以使用 前（a）后(a)
无论是a 还是 a都会立即使原变量自减1
不同的是a和a的值是不同的，
--a的值是变量的新值（自减后的值）
a--的值是变量的原值（自减前的值）

#### 逻辑运算符

!
非运算可以对一个布尔值进行取反，true变false false边true
当对非布尔值使用!时，会先将其转换为布尔值然后再取反
我们可以利用!来将其他的数据类型转换为布尔值

&&
&&可以对符号两侧的值进行与运算
只有两端的值都为true时，才会返回true。只要有一个false就会返回false。
与是一个短路的与，如果第一个值是false，则不再检查第二个值
对于非布尔值，它会将其转换为布尔值然后做运算，并返回原值

规则：
1.如果第一个值为false，则返回第一个值
2.如果第一个值为true，则返回第二个值

||
||可以对符号两侧的值进行或运算
只有两端都是false时，才会返回false。只要有一个true，就会返回true。
或是一个短路的或，如果第一个值是true，则不再检查第二个值
对于非布尔值，它会将其转换为布尔值然后做运算，并返回原值

#### 赋值运算符

=
可以将符号右侧的值赋值给左侧变量

+=

```js
a += 5 相当于 a = a+5    
var str = "hello";  str += "world";
```

-=

```js
a -= 5  相当于 a = a-5
```

*=

```js
a *= 5 相当于 a = a*5
```

/=

```js
a /= 5 相当于 a = a/5
```

%=

```js
a %= 5 相当于 a = a%5
```

#### 关系运算符

关系运算符用来比较两个值之间的大小关系的
\>
\>=
<
<=
关系运算符的规则和数学中一致，用来比较两个值之间的关系，
如果关系成立则返回true，关系不成立则返回false。
如果比较的两个值是非数值，会将其转换为Number然后再比较。
如果比较的两个值都是字符串，此时会比较字符串的Unicode编码，而不会转换为Number。

#### 相等运算符

==相等，判断左右两个值是否相等，如果相等返回true，如果不等返回false
相等会自动对两个值进行类型转换，如果**对不同的类型进行比较，会将其转换为相同的类型然后再比较**，转换后相等它也会返回true，null == undefined

!=
不等，判断左右两个值是否不等，如果不等则返回true，如果相等则返回false
不等也会做自动的类型转换。

**===全等**，判断左右两个值是否全等，它和相等类似，只不过它不会进行自动的类型转换，
如果两个值的类型不同，则直接返回false

**!==不全等**，和不等类似，但是它不会进行自动的类型转换，如果两个值的类型不同，它会直接返回true

特殊的值：
null和undefined
由于undefined衍生自null，所以**null == undefined** 会返回true。
但是 null === undefined 会返回false。

**NaN**
NaN不与任何值相等，报告它自身 NaN == NaN //false

判断一个值是否是NaN：使用isNaN()函数

#### 三元运算符：

?:
语法：条件表达式?语句1:语句2;
执行流程：
先对条件表达式求值判断，
如果判断结果为true，则执行语句1，并返回执行结果
如果判断结果为false，则执行语句2，并返回执行结果

优先级：
和数学中一样，JS中的运算符也是具有优先级的，
比如 先乘除 后加减 先与 后或
具体的优先级可以参考优先级的表格，在表格中越靠上的优先级越高，
优先级越高的越优先计算，优先级相同的，从左往右计算。
优先级不需要记忆，如果越到拿不准的，使用()来改变优先级。

#### 流程控制语句

程序都是自上向下的顺序执行的，
通过流程控制语句可以改变程序执行的顺序，或者反复的执行某一段的程序。

##### 条件分支语句

条件判断语句也称为if语句
语法一：

```js
if(条件表达式){  
	语句...  
}
//执行流程：  
//if语句执行时，会先对条件表达式进行求值判断，  
//如果值为true，则执行if后的语句  
//如果值为false，则不执行
```

语法二：

~~~js
if(条件表达式){  
	语句...  
}else{  
	语句...  
}
   // 执行流程：  
//if...else语句执行时，会对条件表达式进行求值判断，  
	//如果值为true，则执行if后的语句  
	//如果值为false，则执行else后的语句
~~~

语法三：

```js
if(条件表达式){  
	语句...  
}else if(条件表达式){  
	语句...  
}else if(条件表达式){  
	语句...  
}else if(条件表达式){  
	语句...  
}else{  
	语句...  
}
    //执行流程  
 //if...else if...else语句执行时，会自上至下依次对条件表达式进行求值判断，  
	//如果判断结果为true，则执行当前if后的语句，执行完成后语句结束。  
	//如果判断结果为false，则继续向下判断，直到找到为true的为止。  
	//如果所有的条件表达式都是false，则执行else后的语句
```

##### switch语句

语法:

```js
switch(条件表达式){  
	case 表达式:  
		语句...  
		break;  
	case 表达式:  
		语句...  
		break;  
	case 表达式:  
		语句...  
		break;  
	default:  
		语句...  
		break;  
}
```

执行流程：
switch…case…语句在执行时，会依次将case后的表达式的值和switch后的表达式的值进行全等比较，如果比较结果为false，则继续向下比较。如果比较结果为true，则从当前case处开始向下执行代码。如果所有的case判断结果都为false，则从default处开始执行代码。

##### 循环语句

通过循环语句可以反复执行某些语句多次
while循环
语法：

```js
while(条件表达式){  
    语句...  
}
```

执行流程：
while语句在执行时，会先对条件表达式进行求值判断，
如果判断结果为false，则终止循环
如果判断结果为true，则执行循环体
循环体执行完毕，继续对条件表达式进行求值判断，依此类推

do…while循环
语法:

```js
do{  
语句...  
}while(条件表达式)
```

执行流程
do…while在执行时，会先执行do后的循环体，然后在对条件表达式进行判断，
如果判断判断结果为false，则终止循环。
如果判断结果为true，则继续执行循环体，依此类推

- 和while的区别：

  while：先判断后执行

  do…while: 先执行后判断

  do…while可以确保循环体至少执行一次。

for循环
语法：

```js
for(①初始化表达式 ; ②条件表达式 ; ④更新表达式){  
    ③语句...  
}
```

死循环

```js
while(true){  

}  
for(;;){  

}
```

##### **循环练习**

###### **练习一：打印图形**

![image-20220218160919011](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220218160919011.png)

```html
    <script type="text/javascript">
        // 向body中输出一个内容
        // document.write("*****<br />");
        for (var i = 0; i < 5; i++) {
            for (var a = 0; a <= i; a++) {
                document.write("*&nbsp;&nbsp;&nbsp;&nbsp;");
            }
            document.write("<br />");
        }
    </script>
```

###### **练习二：选出全部质数**

```html
<script type="text/javascript">
        var flag = true;
        var num = prompt("请输入一个大于一的整数");
        if (num <= 1)
            alert("该值不合法");
        else {
            for (var i = 2; i < num; i++) {
                if (num % i == 0) {
                    alert(num + "不是质数");
                    flag = false;
                }
            }
            if (flag) alert(num + "是质数");
        }
    </script>
```

###### **练习三：打印9*9乘法表**

```html
  <script type="text/javascript">
        for (var i = 1; i <= 9; i++) {
            for (var a = 1; a <= i; a++) {
                document.write(a + "*" + i + "=" + i * a + "&nbsp;&nbsp");
            }
            document.write("<br />");
        }
    </script>
```

##### break

- break关键字可以用来退出**switch或循环语句**
- 不可以用在if里面
- 会立即终止离他最近的循环语句
- 终止指定循环
  - 可以为循环创建一个label，来标识当前的循环
  - label:循环语句
  - 使用break语句时，可以在break后跟着一个label
  - 这样break将会结束指定的循环，而不是最近的

```js
outer:
        for (var i = 0; i < 5; i++) {
            console.log("外层循环" + i);
            for (var a = 0; a < 5; a++) {
                break outer;
                console.log("内层循环")
            }
        }
```

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220218162047911.png" alt="image-20220218162047911" style="zoom: 67%;" />

如果不加break outer

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220218162115466.png" alt="image-20220218162115466" style="zoom:67%;" />

##### continue

- continue用于跳过当次循环
- continue也是默认只对离他最近的循环起作用

```js
for (var i = 0; i < 5; i++) {
            if (i == 2) {
                continue;
            }
            console.log(i);
        }
// 0 1 3 4 
```

### 5 对象

- 对象不是基本数据类型
- 基本数据类型都是单一的值
- 对象是JS中的引用数据类型
- **对象是一种复合数据类型，在对象中可以保存多个不同数据类型的属性**
- 使用typeof检查一个对象时，会返回object

#### 对象分类

1. 内建对象
   \- 由ES标准中定义的对象，在任何的ES的实现中都可以使用
   \- 比如：Math String Number Boolean Function Object….

2. 宿主对象
   \- 由JS的运行环境提供的对象，目前来讲主要指由浏览器提供的对象
   \- 比如 BOM DOM  console.log document.write

3. 自定义对象

   ```
   - 由开发人员自己创建的对象  
   ```

创建对象
方式一：

```js
var obj = new Object();
//使用new关键字调用的函数，是构造函数constructor
//构造函数是专门用来创建对象的函数
```

方式二：

```js
var obj = {};
```

#### **向对象中添加属性**

语法：
对象.属性名 = 属性值;

**对象的属性名没有任何要求，不需要遵守标识符的规范，但是在开发中，尽量按照标识符的要求去写。**

```js
obj.name = "孙悟空";
```

#### **读取对象中的属性**

语法：
对象.属性名
对象[“属性名”] //“属性名”可以使字符串常量，也可以是字符串变量
如果读取一个对象中没有的属性，它不会报错，而是返回一个undefined

#### **删除对象中的属性**

语法：

```js
delete 对象.属性名  
delete 对象["属性名"]
```

```js
// 使用typeof检查一个对象时，会返回一个object
var obj = new Object();
// 在对象中保存的值为属性
// 向对象中添加属性：
// 语法：  对象.属性名  = 属性值
obj.name = "sunwukong";
obj.gender = "男";
obj.age = 18;
// 如果读取对象中没有的属性，不会报错，而会返回undefined
console.log(obj.name);
// 修改对象属性
obj.name = "zhubajie";
console.log(obj.name);
// 删除对象属性
// 语法： delete 对象.属性
delete obj.name;
console.log(obj.name);
```

#### 属性名和属性值需要注意的点

- **对象[“属性名”] = 属性值;** //这种方式能够使用特殊的属性名
- 读取时也用这种方法
- 使用[]这种形式去操作属性，更加的灵活
- 在[]中可以直接传递一个变量，这样变量值是多少就会读取哪个属性
- 属性值也可以任意的数据类型，甚至也可以是一个对象。

```js
 var obj = new Onject();
// 对象的属性名没有任何要求，不需要遵守标识符的规范，但是在开发中，尽量按照标识符的要求去写。
// 对象[“属性名”] = 属性值;** //这种方式能够使用特殊的属性名
// 读取时也用这种方法
// 使用[]这种形式去操作属性，更加的灵活
// 在[]中可以直接传递一个变量，这样变量值是多少就会读取哪个属性
obj["123"] = 789;
obj["nihao"] = "你好";
var n = "123";
console.log(obj[n]);
//789
```

#### 检查对象中是否含有指定属性

**in 运算符**

```js
// 属性名 in 对象
console.log("test2" in obj);//false
console.log("test" in obj);//true
```

#### 基本数据类型和引用数据类型

> 本质就一句话 :基本数据类型保存的是值,引用数据类型保存的是地址

- 基本数据类型：

  - String Number Boolean Null Undefined

- 引用数据类型：

  - Object

- **基本数据类型的数据，变量是直接保存的它的值。**

  - 变量与变量之间是互相独立的，修改一个变量不会影响其他的变量。
  - <img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220218185834171.png" alt="image-20220218185834171" style="zoom: 67%;" />

- **引用数据类型的数据，变量是保存的对象的引用（内存地址）。**

  - 如果多个变量指向的是同一个对象，此时修改一个变量的属性，会影响其他的变量。
  - 比较两个变量时，对于基本数据类型，比较的就是值，
  - 对于引用数据类型比较的是地址，地址相同才相同

  ```js
  // JS中的变量是保存在栈内存中
  // 基本数据类型的值直接保存在栈内存中储存
  // 值与值之间是独立存在的,修改一个变量不会影响其他的变量
  
  // 对象是保存到堆内存中的,每创建一个新的对象,就会在堆内存中开辟一个新的空间
  // 而变量保存的是对象的内存地址(对象的引用),如果两个变脸保存的是同一个变量的引用
  // 当通过一个变量修改对象的属性的时候,另一个也会受到影响
  var obj = new Object();
  obj.name = "zhubajie"
  var obj2 = obj;
  obj.name = "shaheshang";
  console.log(obj2.name);//shaheshang
  
  obj2 = null;
  console.log(obj.name);//shaheshang
  
  var obj3 = new Object();
  obj3.name = "shaheshang";
  console.log(obj3 == obj);//false
  ```

  

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220218190358140.png" alt="image-20220218190358140" style="zoom:67%;" />

​	

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220218190623288.png" alt="image-20220218190623288" style="zoom:67%;" />

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220218190850093.png" alt="image-20220218190850093" style="zoom:67%;" />

#### 对象字面量

使用对象字面量来创建一个对象

```js
var obj = {};
/*
使用对象字面量,可以在创建对象时,直接指定对象中的属性
语法:{属性名:属性值,属性名:属性值....}
使用对象字面量,可以在创建对象时,直接指定对象中的属性
语法:{属性名:属性值,属性名:属性值....}
对象字面量的属性名可以加引号也可以不加,建议不加
如果要使用一些特殊的名字,则必须加引号

属性名和书信之时一组一组的名值对结构,隔开
如果一个属性之后没有其他的属性了,就不要写,
*/
var obj2 = { 
    name: "猪八戒",
    age: 28 
};
console.log(obj2);
```

### 6 函数

**函数也是一个对象，也具有普通对象的功能（能有属性）**
函数中可以封装一些代码，在需要的时候可以去调用函数来执行这些代码
使用typeof检查一个函数时会返回function
**创建函数**
函数声明

```js
function 函数名([形参1,形参2...形参N]){  
语句...  
}
```

函数表达式

```js
var 函数名 = function([形参1,形参2...形参N]){  
语句...  
};
```

调用函数
语法：函数对象([实参1,实参2…实参N]);
fun() sum() alert() Number() parseInt()
当我们调用函数时，函数中封装的代码会按照编写的顺序执行

**立即执行函数**
函数定义完，立即被调用，这种函数叫做立即执行函数
立即执行函数往往只会执行一次

```js
(function(a,b){  
    console.log("a = "+a);  
    console.log("b = "+b);  
})(123,456);
```

遍历对象

```js
for(var v in obj){  
    document.write("property：name ="+v+"value="+obj[v]+"<br/>" );  
}
```

形参和实参
形参：形式参数
定义函数时，可以在()中定义一个或多个形参，形参之间使用,隔开
定义形参就相当于在函数内声明了对应的变量但是并不赋值，
形参会在调用时才赋值。

实参：实际参数
调用函数时，可以在()传递实参，传递的实参会赋值给对应的形参,
调用函数时JS解析器不会检查实参的类型和个数，可以传递任意数据类型的值。
**如果实参的数量大于形参，多余实参将不会赋值，**
**如果实参的数量小于形参，则没有对应实参的形参将会赋值undefined**

**返回值，就是函数执行的结果。**
使用return 来设置函数的返回值。
语法：return 值;
该值就会成为函数的返回值，可以通过一个变量来接收返回值
return后边的代码都不会执行，一旦执行到return语句时，函数将会立刻退出。
return后可以跟任意类型的值，可以是基本数据类型，也可以是一个对象。
**如果return后不跟值，或者是不写return则函数默认返回undefined。**
break、continue和return
break
退出循环
continue
跳过当次循环
return
退出函数

**参数，函数的实参也可以是任意的数据类型。**

参数也可以是函数，在开发中也会经常用到

```js
function fun(a){
    console.log(a);
}
fun(function(){alert("hello")});//打印function(){alert("hello")}
fun()
```

**fun() 和 fun的区别**

- fun()是调用函数，相当于使用的是函数的返回值
- fun是函数对象

**函数的返回值也可以是函数**

```js
function fun3(){
    //在函数内部声明一个函数
    function fun4(){
        alert("我是fun4");
    }
    //将fun4函数对象作为返回值返回
    return fun4;
}

a = fun3();
//console.log(a);  输出的是fun4
a() ;//调用了fun4()
fun3()();//调用了fun4()
```

### 7  作用域

作用域简单来说就是一个变量的作用范围。
在JS中作用域分成两种：

1. 全局作用域

- 直接在script标签中编写的代码都运行在全局作用域中
  **全局作用域在打开页面时创建，在页面关闭时销毁。**

- 全局作用域中有一个全局对象window，window对象由浏览器提供，
  可以在页面中直接使用，它代表的是整个的浏览器的窗口。

- **在全局作用域中创建的变量都会作为window对象的属性保存**

  在全局作用域中创建的函数都会作为window对象的方法保存
  在全局作用域中创建的变量和函数可以在页面的任意位置访问。
  在函数作用域中也可以访问到全局作用域的变量。
  **尽量不要在全局中创建变量**

2. 函数作用域

- 函数作用域是函数执行时创建的作用域，每次调用函数都会创建一个新的函数作用域，他们之间是相互独立的。函数作用域在函数执行时创建，在函数执行结束时销毁。

- 在函数作用域中创建的变量，不能在全局中访问。
  当在函数作用域中使用一个变量时，它会先在自身作用域中寻找，
  如果找到了则直接使用，如果没有找到则到上一级作用域中寻找，
  如果找到了则使用，找不到则继续向上找，一直会

- 定义形参就相当于在函数作用域中声明变量

  ```js
  var e = 123;
  function fun(e){
      console.log(e);//undefined
  }
  ```

  

**变量的声明提前**

- 在全局作用域中，使用**var关键字声明的变量会在所有的代码执行之前被声明，但是不会赋值**
- 所以我们可以在变量声明前使用变量。但是不使用var关键字声明的变量不会被声明提前。
- 在函数作用域中，也具有该特性，使用var关键字声明的变量会在函数所有的代码执行前被声明，
- 如果没有使用var关键字声明变量，则变量会变成全局变量

```js
console.log(a);
var a = 123;//undefined  在所有的代码执行之前被声明，但是不会赋值

console.log(a);
a = 123;//报错
```

**函数的声明提前**

- 在全局作用域中，使用**函数声明创建的函数（function fun(){}）,会在所有的代码执行之前被创建**，也就是我们可以在函数声明前去调用函数

```js
funciton 函数名(){}
```

- 但是使用函数表达式(var fun = function(){})创建的函数没有该特性（funciton创建了，但是没有赋值给fun）
- 在函数作用域中，使用函数声明创建的函数，会在所有的函数中的代码执行之前就被创建好了。

### 8 this（上下文对象）

我们每次调用函数时，解析器都会将一个上下文对象作为隐含的参数传递进函数。
使用this来引用上下文对象，根据函数的调用形式不同，this的值也不同。

指向当前对象：

this的不同的情况：

1. 以函数的形式调用时，this是window
2. 以方法的形式调用时，this就是调用方法的对象
3. 以构造函数的形式调用时，this就是新创建的对象

### 9 构造函数

- 创建一个构造函数,专门用来创建Person对象
- 构造函数就是 一个普通的函数,创建方式和普通函数没有区别
- 不同的是构造函数习惯上首字母大写
- 构造函数和普通函数的区别就是调用方式的不同
  - 普通函数是直接调用
  - 构造函数需要使用new关键字
- **构造函数的执行流程:**

1. 立刻创建一个新的对象
2. 将新建的对象设置为函数的this,在构造函数中可以使用this来引用新建的对象
3. 执行函数中的代码
4. 将新建的对象作为返回值返回

```js
 function Person(name, age, gender) {
     // name = "hello" 这是往全局中添加
     this.name = name;
     this.age = age;
     this.gender = gender;
     this.sayName = function () {
         alert(this.name);
     }
 }
var per = new Person();
```

- 使用同一个构造函数创建的对象,我们成为一类对象,也将一个构造函数成为一个类。我们将通过一个构造函数创建的对象成为是该类的实例

- **instanceof 可以检查一个对象是否是一个类的实例**
  对象 instanceof 构造函数  如果是,则返回true
- **所有的对象都是object的后代**
  所以任何对象和object做instanceof检查时返回都时true

### 10 原型对象

创建一个函数以后，**解析器都会默认在函数中添加一个属性prototype**

prototype属性指向的是一个对象，这个对象我们称为原型对象。

当函数作为构造函数使用，**它所创建的对象中都会有一个隐含的属性执行该原型对象。**

```
这个隐含的属性可以通过对象.__proto__来访问。
```

![image-20220220151906647](C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220220151906647.png)

- 如果函数作为普通函数调用，prototype没有任何作用
- 当函数以构造函数的形式调用时，它所创建的对象中都会有一个隐含属性
  - 隐含属性指向该构造函数的原型对象，我们可以通过`__proto__`来访问
- 原型对象就相当于一个公共区域，所有同一个类的实例都可以访问到这个原型对象，
  - 我们可以将对象中共有的内容，统一添加到原型对象中。
  - 当我们去访问对象的一个属性或调用对象的一个方法时，它会先自身中寻找，
    如果在自身中找到了，则直接使用。
    如果没有找到，则去原型对象中寻找，如果找到了则使用
- **以后创建构造函数时，可以将对象中共有的属性和方法统一添加到原型对象中。**
  - 这样写的好处是：不用分别为每一个对象添加，还不会污染全局作用域，就可以使每个对象都具有这样的属性和方法了。

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220220154541080.png" alt="image-20220220154541080" style="zoom:67%;" />

- 当我们去访问对象的一个属性或调用对象的一个方法时，它会先自身中寻找，
  - 如果在自身中找到了，则直接使用。
  - 如果没有找到，则去原型对象中寻找，如果找到了则使用，
  - **如果没有找到，则去原型的原型中寻找，**依此类推。直到找到Object的原型为止，Object的原型的原型为null，如果在object 中依然没有找到，则返回undefined

<img src="C:\Users\fy\AppData\Roaming\Typora\typora-user-images\image-20220220154903360.png" alt="image-20220220154903360" style="zoom: 50%;" />

```js
console.log(mc.hasOwnProperty("name"));//false
console.log(mc.__proto__.hasOwnProperty("hasOwnProperty"))//false
console.log(mc.__proto__.__proto__.hasOwnProperty("hasOwnProperty"))//true
console.log(mc.__proto__.__proto__.__proto__)//null
```

### 11 toString方法

------

当我们直接在页面中打印一个对象时，事件上是输出的对象的toString()方法的返回值：[object Object]

如果我们希望在输出对象时不输出[object Object]，可以为对象添加一个toString()方法

```js
//修改Person原型的toString  
Person.prototype.toString = function(){  
	return "Person[name="+this.name+",age="+this.age+",gender="+this.gender+"]";  
};
```

### 12 垃圾回收

------

就像人生活的时间长了会产生垃圾一样，程序运行过程中也会产生垃圾这些垃圾积攒过多以后，会导致程序运行的速度过慢，所以我们需要一个垃圾回收的机制，来处理程序运行过程中产生垃圾
**当一个对象没有任何的变量或属性对它进行引用，此时我们将永远无法操作该对象，**此时这种对象就是一个垃圾，这种对象过多会占用大量的内存空间，导致程序运行变慢，所以这种垃圾必须进行清理。在JS中拥有自动的垃圾回收机制，会自动将这些垃圾对象从内存中销毁，
**我们不需要也不能进行垃圾回收的操作我们需要做的只是要将不再使用的！对象！设置null即可**！

### 13 数组

------

**数组**

- 数组也是一个对象，是一个用来存储数据的对象和Object类似，但是它的存储效率比普通对象要高
- 普通对象时是使用字符串作为属性名的,而数组是使用数字来作为索引来操作元素的
- 数组中保存的内容我们称为元素
- 数组使用索引（index）来操作元素
- 索引指由0开始的整数

#### 13.1 数组操作

**创建数组**

```js
var arr = new Array();
var arr = []//使用字面量创建数组,更方便
```

**向数组中添加元素**
语法:数组对象[索引] = 值;

```js
arr[0] = 123;  arr[1] = "hello";
```

**创建数组时直接添加元素**
语法：

```js
var arr = [元素1,元素2....元素N];
```

例子：

```js
var arr = [123,"hello",true,null];
//或者 var arr = new Array(123,"hello",true,null)
//注意 var arr = new Array(10)  创建一个长度为10 的数组
```

**数组中的元素可以是任意的数据类型,也可以是对象**

#### 13.2 获取和修改数组的长度

> **使用length属性来操作数组的长度**

- **获取长度：数组.length**
  - length获取到的是数组的最大索引+1
  - 对于连续的数组，length获取到的就是数组中元素的个数

- **修改数组的长度数组.length = 新长度**
  - 如果修改后的length大于原长度，则多出的部分会空出来
  - 如果修改后的length小于原长度，则原数组中多出的元素会被删除
- 向数组的最后添加元素: 数组[数组.length] = 值;

#### 13.3 数组的方法

| functionName |                        function                        |                  usage                  |
| :----------- | :----------------------------------------------------: | :-------------------------------------: |
| push()       | 用来向数组的末尾添加一个或多个元素，并返回数组新的长度 | 语法：数组.push(元素1,元素2,元素N)pop() |
| pop()        |     用来删除数组的最后一个元素，并返回被删除的元素     |                                         |
| unshift()    |  向数组的开头添加一个或多个元素，并返回数组的新的长度  |                                         |
| shift()      |      删除数组的开头的一个元素，并返回被删除的元素      |                                         |
| reverse()    |       可以用来反转一个数组，它会对原数组产生影响       |                                         |

#### 13.4 遍历数组

`for...in`循环不仅可以遍历对象，也可以遍历数组，毕竟数组只是一种特殊对象。

```js
var a = [1, 2, 3];
for (var i in a) {
  console.log(a[i]);
}
// 1
// 2
// 3
```

但是，`for...in`不仅会遍历数组所有的数字键，还会遍历非数字键。所以，不推荐使用`for...in`遍历数组。

数组的遍历可以考虑使用`for`循环或`while`循环。

```js
var a = [1, 2, 3];

// for循环
for(var i = 0; i < a.length; i++) {
  console.log(a[i]);
}

// while循环
var i = 0;
while (i < a.length) {
  console.log(a[i]);
  i++;
}

var l = a.length;
while (l--) {
  console.log(a[l]);
}
```

上面代码是三种遍历数组的写法。最后一种写法是逆向遍历，即从最后一个元素向第一个元素遍历。

#### 13.5 **for each **

- 数组的`forEach`方法，(只支持ie8以上的)用来遍历数组，详见《标准库》的 Array 对象一章。
- `forEach`需要一个函数作为参数,像这种函数有我们创建但是不由我们调用的,称为回调函数
- 数组中有几个元素，回调函数就会被调用几次
- 每次调用时，都会将遍历到的信息以实参的形式传递进来,我们可以定义形参来获取这些信息。
  - value:正在遍历的元素
  - index:正在遍历元素的索引
  - obj:被遍历对象

```js
数组.forEach(function(value , index , obj){    
});
var colors = ['red', 'green', 'blue'];
colors.forEach(function (color) {
  console.log(color);
});
// red
// green
// blue
```

#### 13.6 slice和splice

```
slice:
可以从一个数组中截取指定的元素  
该方法不会影响原数组，而是将截取到的内容封装为一个新的数组并返回  
参数：  
   1.截取开始位置的索引（包括开始位置）  
   2.截取结束位置的索引（不包括结束位置）  
    第二个参数可以省略不写，如果不写则一直截取到最后  
    参数可以传递一个负值，如果是负值，则从后往前数  
```

```
splice:
可以用来删除数组中指定元素，并使用新的元素替换  
该方法会将删除的元素封装到新数组中返回  
参数：  
   1.删除开始位置的索引  
   2.删除的个数  
   3.三个以后，都是替换的元素，这些元素将会插入到开始位置索引的前边  
```

#### 13.7 数组的其他方法

```js
concat()
可以连接两个多多个数组,并将新数组返回
不会对原数组产生影响
var arr = ["","",""];
var arr1 = ["","",""];
var arr2 = ["","",""];
var result = arr.concat(arr1,arr2,"","","");
```

```
join([splitor])
可以将一个数组转换为一个字符串
不会对原数组产生影响,而是将新数组返回
可以指定一个字符串作为参数，这个字符串将会作为连接符来连接数组中的元素
如果不指定连接符则默认使用
var arr = ["辣辣辣","啦啦啦","拉拉拉"];
var result = arr.join();//辣辣辣,啦啦啦,拉拉拉
result = arr.join('*');//辣辣辣*啦啦啦*拉拉拉
```

```js
sort()
可以对一个数组中的内容进行排序，默认是按照Unicode编码进行排序
即使对纯数字的数组,使用sort()排序时,也会按照Unicode编码来排序,所以对数字进行排序可能会得到错误的结果
调用以后，会直接修改原数组。
可以自己指定排序的规则，需要一个回调函数作为参数：

我们可以自己来指定排序的规则
我们可以在sort()添加一个回调函数，来指定排序规则，
回调函数中需要定义两个形参,
浏览器将会分别使用数组中的元素作为实参去调用回调函数
使用哪个元素调用不确定，但是肯定的是在数组中a一定在b前边

浏览器会根据回调函数的返回值来决定元素的顺序，
如果返回一个大于0的值，则元素会交换位置
如果返回一个小于0的值，则元素位置不变
如果返回一个0，则认为两个元素相等，也不交换位置

如果需要升序排列，则返回a-b
如果需要降序排列，则返回b-a

arr.sort(function(a,b){  
	//升序排列  
	return a-b;  
	  
	//降序排列  
	return b-a;  
})
```

```js
reverse()
反转数组
该方法直接修改原数组
```

### 14 call 和 apply

- 这两个方法都是函数对象的方法，需要通过函数对象来调用。

- 当对函数调用call和apply都会调用函数执行

- 在调用call和apply 可以将一个对象指定为第一个参数

  - 此时这个对象将会成为函数执行时的this

- call()方法可以将实参在对象之后依次传递

- apply()方法需要将实参分装到一个数组中统一传递

  ```js
  function fun() {
      alert(this);
  }
  function say(a, b) {
      console.log("a: " + a);
      console.log("b: " + b);
  }
  var obj = {};
  fun.call(obj);
  fun.apply(obj);
  say.call(obj, 2, 3);
  say.apply(obj, [2, 3]);
  ```

- this的情况：
  - 以函数形式调用时，this 是windows
  - 以方法形式调用时，this 是方法的对象
  - 以构造函数的形式调用时，this是新的对象
  - 使用call 和apply 调用时，this是指定的对象

### 15 arguments

在嗲用函数时，浏览器每次都会传递两个隐含的参数

1.  函数的上下文对象this
2. 封装实参的对象arguments
   - arguments是一个类数组对象，也可以通过索引操作数据，也可以获取长度
   - 在调用函数时，我们多传递的实参都会在arguments中保存
   - arguments.length可以获取实参的数量
   - 即使不定义形参，也可以通过arguments 来说使用实参
     - 只不过比较麻烦
     - arguments[0]表示第一个参数
     - arguments[1]表示第二个参数
   - 它里边有一个属性叫做callee
     - 这个属性对应一个函数对象，就是当前正在指向的函数对象

### 16 date对象

日期的对象，在JS中通过Date对象来表示一个时间
创建对象
创建一个当前的时间对象

```js
var d = new Date();
//如果直接使用构造函数创建一个Date对象，则会封装为当前代码的执行时间
```

创建一个指定的时间对象

```js
var d = new Date("月/日/年 时:分:秒");
```

**方法**

| name              |                                                              |
| :---------------- | :----------------------------------------------------------- |
| getDate()         | 当前日期对象是几日（1-31）                                   |
| getDay()          | 返回当前日期对象时周几（0-6） 0 周日 1 周一 。。。           |
| getMonth()        | 返回当前日期对象的月份（0-11） 0 一月 1 二月 。。。          |
| getFullYear()     | 从 Date 对象以四位数字返回年份。                             |
| getHours()        | 返回 Date 对象的小时 (0 ~ 23)。                              |
| getMinutes()      | 返回 Date 对象的分钟 (0 ~ 59)。                              |
| getSeconds()      | 返回 Date 对象的秒数 (0 ~ 59)。                              |
| getMilliseconds() | 返回 Date 对象的毫秒(0 ~ 999)。                              |
| getTime()         | 返回当前日期对象的时间戳 时间戳，指的是从1970年月1日 0时0分0秒，**到现在时间的毫秒数** 计算机底层保存时间都是以时间戳的形式保存的。 |
| Date.now()        | 可以获取当前代码执行时的时间戳                               |
| setHours()        | 设置 Date 对象中的小时 (0 ~ 23)                              |

### 17 Math

- Math属于一个工具类，它不需要我们创建对象，它里边封装了属性运算相关的常量和方法
  我们可以直接使用它来进行数学运算相关的操作
- 不是构造函数，不用创建对象

方法：
Math.PI
常量，圆周率
Math.abs()
绝对值运算
Math.ceil()
向上取整
Math.floor()
向下取整
Math.round()
四舍五入取整
Math.random()
生成一个01之间的随机数
生成一个xy之间的随机数
Math.round(Math.random()*(y-x)+x);
Math.pow(x,y)
求x的y次幂
Math.sqrt()
对一个数进行开方
Math.max()
求多个数中最大值
Math.min()
求多个数中的最小值

| 方法                                   | 作用                                |
| -------------------------------------- | ----------------------------------- |
| Math.abs()                             | 计算一个数的绝对值   Math.abs(-1)   |
| Math.ceil()                            | 向上取整，小数位只要有值，就自动进1 |
| Math.floor()                           | 向下取整                            |
| Math.round()                           | 四舍五入取整                        |
| Math.random()                          | 生成一个01之间的随机数              |
| **Math.round(Math.random()*(y-x)+x);** | 生成一个xy之间的随机数              |
| Math.pow(x,y)                          | 求x的y次幂                          |
| Math.sqrt()                            | 对一个数进行开方                    |
| Math.max(10，20，30)                   | 求多个数中最大值                    |
| Math.min()                             | 求多个数中最小值                    |

### 18 包装类

在JS中提供了三个包装来，通过着三个包装类可以将基本数据类型的数据转化为对象

- string()

  - 可以将基本数据类型字符串转换为String对象

- Number()

  - 可以将基本数据类型数字转换为Number 对象

- boolean()

  - 可以将基本数据类型布尔值转换为boolean对象

- 在实际应用中，不会使用基本数据类型的对象。如果使用基本数据类型的对象，在做比较时可能会带来一些不可预期的结果，因为是不同的对象

- 使用：

  ```js
  //方法和属性只能添加给对象，不能添加给基本数据类型
  //当我们对一些基本数据类型的值去掉用属性和方法时，
  //浏览器会临时使用包装类将其转化为对象，然后再调用对象的属性和方法。
  //调用完之后转换为基本数据类型
  var a = 123;
  s = s.toString();
  
  console.log(s);"123"
  console.log(typeof(s));string
  ```

### 19 String 方法

```
在底层字符串是以字符数组的形式保存的
["H","e"]
```

| 属性       | 使用             |
| ---------- | ---------------- |
| length属性 | 获取字符串的长度 |

| 方法               | 使用                                                         |
| ------------------ | ------------------------------------------------------------ |
| charAt()           | 根据索引获取指定的字符                                       |
| charCodeAt()       | 根据索引获取指定的字符Unicode编码                            |
| fromcharCode()     | String.fromcharCode(73)根据Unicode编码获取字符               |
| indexOf()          | 从一个字符串中检索指定内容  返回的是第一次出现的索引，如果没有找到则返回-1。可以指定一个第二个参数，来表示开始查找的位置 |
| lastIndexOf()      | indexOf()是从前向后找，lastIndexOf()是从后向前找             |
| slice[start,[end]) | 可以从一个字符串中截取指定的内容，并将截取到内容返回，不会影响原变量。参数：<br/>第一个：截取开始的位置（包括开始）<br/>第二个：截取结束的位置**（不包括结束）**<br/>可以省略第二个参数，如果省略则一直截取到最后<br/>可以传负数，如果是负数则从后往前数 |
| substr()           | 和slice()基本一致，不同的是它第二个参数不是索引，而是截取的数量 |
| substring()        | 和slice()基本一致，不同的是它不能接受负值作为参数，如果设置一个负值，则会自动修正为0， |
| toLowerCase()      | 将字符串转换为小写并返回                                     |
| toUpperCase()      | 将字符串转换为大写并返回                                     |

### 20 正则表达式

正则用来定义一些字符串的规则，程序可以根据这些规则来判断一个字符串是否符合规则，

也可以将一个字符串中符合规则的内容提取出来。

**创建正则表达式对象**

```js
var reg = new RegExp(“正则”,”匹配模式”); 
```

### 21 回调函数

#### 21.1 什么是回调函数

- 你定义的
- 你没有调
- 但最终它执行了(在某个时刻或某个条件下)

#### 21.2 常见的回调函数

- dom事件回调函数 ==>发生事件的dom元素
- 定时器回调函数 ===>window
- ajax请求回调函数(后面讲)
- 生命周期回调函数(后面讲)

```js
// dom事件回调函数
 document.getElementById('btn').onclick = function () {alert(this.innerHTML)}
 // 定时器回调函数
 setTimeout(function () {   alert('到点了'+this)}, 2000)
```

