---
title: vue采坑之旅
date: 2018-03-21 14:23:27
tags:
---

年前做的零售户，是基于vue-cli 和 webpack的单页应用，部署到nginx服务器之后需要在线上起前端node服务。但是会出现前端服务偶尔挂掉的情况，real尴尬...

之后通过build生成静态资源(index.html + static文件夹)，并放到服务器上，可是这没有办法满足路由切换的需求。另外，由于vue-cli只提供了build这一种方法，在build.js中设置process.env.NODE_ENV = 'production'，其实在线上跑的服务仍然是用“npm run dev”，这会使得程序认为环境还是development。__webpack_hmr 则一直是 404.

所以，接下来就改造一下vue-cli的脚手架吧~

npm run dev
找到 dev-server.js

延伸：
npm 常用模块
    chalk 命令行彩色输出 var chalk = require('chalk')
    opn 自动用浏览器打开相应路径 var opn = require('opn')
    path 路径模块
    http-proxy-middleware 单线程node.js代理中间件，用于连接，快速和浏览器同步

    var proxy = require('http-proxy-middleware')
    var apiProxy = proxy('/api', {target: 'http://www.example.org'});
    //                   \____/   \_____________________________/ 
    //                     |                    | 
    //                   context             options 
    // context：确定应将哪些请求代理到目标主机
    // options.target：目标主机到代理
    // proxy middleware options 
    var options = {
            target: 'http://www.example.org', // target host 
            changeOrigin: true,               // needed for virtual hosted sites 
            ws: true,                         // proxy websockets 
            pathRewrite: {
                '^/api/old-path' : '/api/new-path',     // rewrite path 
                '^/api/remove/path' : '/path'           // remove base path 
            },
            router: {
                // when request.headers.host == 'dev.localhost:3000', 
                // override target 'http://www.example.org' to 'http://localhost:8000' 
                'dev.localhost:3000' : 'http://localhost:8000'
            }
        };

  var express = require('express')
  var app = express()
  express框架简历在node.js内置的http模块上
  中间件，说白了就是处理http请求的函数. use是express处理中间件的方法，它返回一个函数.针对不同请求，express提供了use方法的一些别名，例如get,post,all等，即HTTP动词都是express的方法。例如：
  app.get('/', middleware)
  middle (req, res, next)三个参数
      