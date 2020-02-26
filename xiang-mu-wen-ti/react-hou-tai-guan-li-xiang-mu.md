# React后台管理项目

## POST [http://localhost:3000/login](http://localhost:3000/login) 500 \(Internal Server Error\)  ECONNREFUSED 

mongodb服务已开启。尝试停止再开启，但无效。后运行代理http://localhost:5000，成功解决。

## Error: Cannot find module 'react-dev-utils/crossSpawn'

删除node-modules文件夹，运行npm install。

原因：有些包之间交叉影响

## 错误为Module build failed \(from ./node\_modules/babel-loader/lib/index.js\)

[https://www.cnblogs.com/xxflz/p/9564846.html](https://www.cnblogs.com/xxflz/p/9564846.html)——使用此博客内的解决办法npm install @babel/core @babel/preset-env后产生上面一个问题

## net::ERR\_ABORTED

心知天气API接口使用错误。后用公钥私钥同时使用，crypto-js加解密的方法解决。

## does not contain a default export \(imported as 'reqWeather'\)

若引入的组件在它声明的文档里并非唯一导出的组件，则需在引入时加上大括号

## git clone时遇到的错误：HttpReQuestException encoutered && repository not found

 Github 禁用了TLS v1.0 and v1.1，必须更新Windows的git凭证管理器。

## net-start-mongodb报错：服务名无效

1.将data目录下的所有文件都删除;

2.以管理员模式打开cmd,cd到mongodb bin目录下,运行:

mongod --config "D:\Mongo\mongo.conf"  --install --serviceName "MongoDB"

## MongoDB net start MongoDB启动,提示发生系统错误 5 拒绝访问 解决之道

cmd管理员启动



