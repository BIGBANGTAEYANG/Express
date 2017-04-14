# Express
==============
### 一、Express学习
1.学习Express之前需要了解的知识有哪些?[链接](https://github.com/BIGBANGTAEYANG/NodeJS_Study/blob/master/README.md)<br>
2.搭建开发环境:<br>
【1】安装Node和Npm[链接](http://www.runoob.com/nodejs/nodejs-install-setup.html);<br>
【2】安装Express[链接](https://www.npmjs.com/package/express);<br>
【3】注意事项:由于版本的原因，很多书上写的Express3.6.X之前的版本，最新是4.15.X版本，之前的版本是将项目构建器模块合并在Express中一起的，后面的版本是将其分开的，独立为一个项目express-generator，所以安装完Express后，只需要再全局安装express-generator项目即可;<br>
【4】安装好express-generator包后，我们在命令行就可以使用express命令了，需要全局安装;<br>
3.快速构建项目步骤:
【1】切换到想要创建项目的目录中，使用命令构建项目,命令express -e 项目名;<br>
【2】切换到创建好的项目目录中，使用命令 npm install,安装项目依赖;<br>
【3】使用命名 npm start 运行项目;<br>
【4】浏览器输入127.0.0.1:3000,即可访问项目页面;<br>
【5】如果运行报错，有可能是可能是express-generator和express不匹配造成的;<br>
4.项目结构解析:
【1】bin,存放启动项目的脚本文件;<br>
【2】node_modules, 存放所有的项目依赖库;<br>
【3】public,静态文件(css,js,img);<br>
【4】routes,路由文件(MVC中的C,controller);<br>
【5】views,页面文件(Ejs模板);<br>
【6】package.json,项目依赖配置及开发者信息;<br>
【7】app.js,应用核心配置文件;<br>
5.文件解析:<br>
【1】wwww文件:有中文注解备注
```javascript
 /**
 * 依赖加载
 */
var app = require('../app');
var debug = require('debug')('expressdemo:server');
var http = require('http');
 /**
 * 定义启动端口
 */

var port = normalizePort(process.env.PORT || '3000');
app.set('port', port);

 /**
 * 创建HTTP服务器实例
 */

var server = http.createServer(app);

 /**
 * 启动网络服务监听端口
 */

server.listen(port);
server.on('error', onError);
server.on('listening', onListening);

/**
 * 端口标准化函数
 */
function normalizePort(val) {
  var port = parseInt(val, 10);

  if (isNaN(port)) {
    // named pipe
    return val;
  }

  if (port >= 0) {
    // port number
    return port;
  }

  return false;
}

 /**
 * HTTP异常事件处理函数
 */

function onError(error) {
  if (error.syscall !== 'listen') {
    throw error;
  }

  var bind = typeof port === 'string'
    ? 'Pipe ' + port
    : 'Port ' + port;

  // handle specific listen errors with friendly messages
  switch (error.code) {
    case 'EACCES':
      console.error(bind + ' requires elevated privileges');
      process.exit(1);
      break;
    case 'EADDRINUSE':
      console.error(bind + ' is already in use');
      process.exit(1);
      break;
    default:
      throw error;
  }
}

 /**
 * 事件绑定函数
 */

function onListening() {
  var addr = server.address();
  var bind = typeof addr === 'string'
    ? 'pipe ' + addr
    : 'port ' + addr.port;
  debug('Listening on ' + bind);
}
```