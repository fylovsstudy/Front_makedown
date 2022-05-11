## node 安装

### nvm

## npm/yarn包管理

## 创建node应用

## node事件

## buffer

如果没有提供编码格式，文件操作以及很多网络操作就会将数据作为 Buffer 类型返回

## Stream

### 理解流

流是基于事件的 API，用于管理和处理数据。

- 流是能够读写的
- 是基于事件实现的一个实例

理解流的最好方式就是想象一下没有流的时候怎么处理数据：

- `fs.readFileSync` 同步读取文件，程序会阻塞，所有数据被读到内存
- `fs.readFile` 阻止程序阻塞，但仍会将文件所有数据读取到内存中
- 希望少内存读取大文件，读取一个数据块到内存处理完再去索取更多的数据

### 流的类型

- 内置：许多核心模块都实现了流接口，如 `fs.createReadStream`
- HTTP：处理网络技术的流
- 解释器：第三方模块 XML、JSON 解释器
- 浏览器：Node 流可以被拓展使用在浏览器
- Audio：流接口的声音模块
- RPC（远程调用）：通过网络发送流是进程间通信的有效方式
- 测试：使用流的测试库

### 使用内建流 API

#### 静态 web 服务器

想要通过网络高效且支持大文件的发送一个文件到一个客户端。

#### 不使用流

```javascript
const http = require('http');
const fs = require('fs');

http.createServer((req, res) => {
  fs.readFile(`${__dirname}/index.html`, (err, data) => {
    if (err) {
      res.statusCode = 500;
      res.end(String(err));
      return;
    }

    res.end(data);
  });
}).listen(8000);
复制代码
```

#### 使用流

```javascript
const http = require('http');
const fs = require('fs');

http.createServer((req, res) => {
  fs.createReadStream(`${__dirname}/index.html`).pipe(res);
}).listen(8000);
复制代码
```

- 更少代码，更加高效
- 提供一个缓冲区发送到客户端



### node模块化与模块记载机制

### node多进程

