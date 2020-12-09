# PM2

PM2 是 node 进程管理工具，可以利用它来简化很多node应用管理的繁琐任务，如性能监控、自动重启、负载 均衡等，而且使用非常简单。

[pm2官网](https://pm2.io/)

## 创建进程的方法

1. **fork**
2. **exec**

## pm2原理

```js
// master
var cluster = require('cluster');
var numCPUs = require('os').cpus().length;

if (cluster.isMaster) {
    console.log(numCPUs);
    for (var i = 0; i < numCPUs; i++) {
        var worker = cluster.fork();
    }
} else {
    require("./app.js");
}
// app.js
// worker
var http = require('http');
http.createServer(function(req, res) {
    res.writeHead(200);
    res.end("hello world\n");
}).listen(8000);
```

pm2 会根据电脑的 cpus 个数去 fork 对应的进程数，Node 多进成默认会采用抢占策略。

::: warning 疑问🤔️
如何检测子进程是否处于正常活跃状态？
:::

**采用心跳检测**，每隔数秒向子进程发送心跳包，子进程如果不回复，那么调用kill杀死这个进程
然后再重新 **cluster.fork()** 一个新的进程

::: warning 疑问🤔️
子进程发出异常报错，如何保证一直有一定数量子进程？
:::

子进程可以监听到错误事件，这时候可以发送消息给主进程，请求杀死自己
并且主进程此时重新调用 **cluster.fork** 一个新的子进程


我们可以依赖 **Nginx**+**pm2**+**docker**来实现自动化+监控部署，