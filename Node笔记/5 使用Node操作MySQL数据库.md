## 使用Node操作Mysql数据库

安装：

```shell
npm install --save mysql
```

使用

启动

```shell
net start mysql
```

启动后才能输入密码访问！

```js
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'me',
  password : 'secret',
  database : 'my_db'
});
 
connection.connect();
 
//'INSERT INTO users VALUES(NULL,"admin","123456")'  插入数据
connection.query('SELECT * FROM `users`', function (error, results, fields) {
  if (error) throw error;
  console.log('The solution is: ', results);
});
 
connection.end();
```

 

