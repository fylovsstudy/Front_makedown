### Mongoose

- 官网：http://mongoosejs.com/
- 官方指南：http://mongoosejs.com/docs/guide.html
- 官方API文档： http://mongoosejs.com/docs/api.html

#### 1. MongoDB数据库的基本概念

- 可以有多个数据库

- 一个数据库中可以有多个集合（表）

- 一个集和中可以有多个文档（表记录）

- 文档结构很灵活，没有限制，不需要像Mysql一样先创建数据库、表、设计表结构

  - 在这里只需要，当你需要插入数据的时候，指定往哪个数据库的哪个集和操作就可以了
  - 一切都由MongoDB来完成自动建库建表这件事

  ```js
  {
      qq:{
          users:[
            {name:"",age:15},  
            {},
            {},
            {},
            .....
          ],
          products:[
              
          ],
          ....
  	},
      taobao:{
          
  	},
      baidu:{
          
      }
  }
  ```

#### 2. 起步

**安装**

```shell
npm i mongoose
```

启动：

```she
mongod
```

hello world

```js
const mongoose = require('mongoose');

//连接mongodb数据库
mongoose.connect('mongodb://localhost:27017/test');

//创建一个模型
//就是在设计数据库
//MongoDB是动态的，非常灵活，只需要在代码中设计你的数据库就可以了
//mongoose这个包就可以让你的设计编写过程变得非常简单
const Cat = mongoose.model('Cat', { name: String });

//实例化一个CAT
const kitty = new Cat({ name: 'Zildjian' });

//持久化保存一个kitty实例
kitty.save().then(() => console.log('meow'));
```

#### 3.官方指南

##### 3.1 设计Schema 发布 Model

```js
var mongoose = require('mongoose')

var Schema = mongoose.Schema

//  1.连接mongodb数据库
mongoose.connect('mongodb://localhost:27017/test');

// 2.设计集和结构 表结构
// 字段名称就是表结构中的属性名称
// 值
const UsersSchema = new Schema({
   username:{
       type:String,
       required:true //必须有
   },
   password:{
       type:String,
       required:true
   },
   email:{
       tpye:String
   }
  });

//   3.将文档结构发布为模型
// mongoose.model方法就是将一个架构发布为model
// 第一个参数：传入一个大写名词字符串用来表示你的数据库
//      mongoose会自动将大写名词的字符串生成小写复数的集合名词
//      例如这里的User最终变成users集合名称
//      第二个参数：架构Schema
// 
//      返回值：模型构造函数
var User = mongoose.model('User',UsersSchema)

// 4.可以使用这个构造函数中的users集和中的数据增删改查

```

##### 3.2 增加数据

```js
var admin = new User(
    {
        username:'admin',
        password:'123456',
        email:'admin@1.com'
    }
)

admin.save(function(err,ret){
    if(err){
        console.log('保存失败')
    }else{
        console.log('保存成功')
        console.log(ret)
    }
})
```

##### 3.3 查询数据

```js
//查询所有
User.find(function(err,data){
    if(err){
        console.log('查询失败')
    }else{
        console.log(data)
    }
})

//按条件查询所有，返回数组
User.find({
    username:'李四'
},function(err,data){
    if(err){
        console.log('查询失败')
    }else{
        console.log(data)
    }
})

//按条件查询单个，返回一个对象
User.findOne({
    username:'李四'
},function(err,data){
    if(err){
        console.log('查询失败')
    }else{
        console.log(data)
    }
})

//_id带"",要去除
 student.findById(req.query.id.replace(/"/g,''),function(err,student){
        if (err){
            res.send('404 Not found')
        }
        res.render('edit.html',{
            student:student
        })
    })
```

##### 3.4 删除数据

```js
 var id = req.query.id.replace(/"/g,'')
    student.findByIdAndRemove(id,function(err,students){
        if (err){
            res.send('404 Not Found')
        }
        res.redirect('/students')
    })
})
```

##### 3.5 更新数据

```js
var id = req.body.id.replace(/"/g,'')
    console.log(id)
    student.findByIdAndUpdate(id,req.body,function(err,students){
        //console.log(req.body)
        if (err){
            console.log('404 Not found')
        }
        res.redirect('/students')
    })
```

