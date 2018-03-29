---
title: vue采坑之旅
date: 2018-03-21 14:23:27
tags:
---

年前做的零售户，是基于vue-cli 和 webpack的单页应用，部署到nginx服务器之后需要在线上起前端node服务。但是会出现前端服务偶尔挂掉的情况，real尴尬...

之后通过build生成静态资源(index.html + static文件夹)，并放到服务器上，可是这没有办法满足路由切换的需求。另外，由于vue-cli只提供了build这一种方式打包构建production环境的页面，在build.js中设置process.env.NODE_ENV = 'production'，其实在线上跑的服务仍然是用“npm run dev”，这使得程序认为环境还是development。__webpack_hmr 则一直是 404.

所以，接下来就改造一下vue-cli的脚手架吧~

问题：1. 路由如何控制，设计到访问页面片段，和页面片段之间的切换

npm run dev
找到 dev-server.js

思路是：写一个 npm run test 和 npm run prod

单页应用如何部署到线上

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

  导航守卫：
  全局的判断需要登录的页面，未登录让用户去登录。
  https://router.vuejs.org/zh-cn/advanced/meta.html

  全局的routes配置只支持 beforeEnter

  单页应用和多页应用的区别。 单页应用的路由，是控制页面片段(组件)之前的切换。

  loadingPage 这个是鸡肋，采用VueRouter统一的切换。类似
    Vue.use(VueLazyload, {
      // loading: require('common/image/default.png')
    })

 this.$refs只有在mounted的时候才能拿到,created的时候拿不到，是空对象。
 掌握生命周期:
    beforeCreate 实例创建之前，什么都还没有
    created 实例创建了，这个阶段已经完成了数据observer，但$el依旧不可见
    beforeMount 开始挂载钩子，但是还没有生成HTML到页面上，标签内任然是Mustach
    mounted el选项的DOM节点被新创建的vm.$el替换,此时实例的数据再dom上进行渲染，html形成。
  window.history.pushState、 window.history.replaceState 和 window.history.go

vuex
action只是commit mutation,
action 通过store.dispatch真正trigger mutation -> state change
the only way to change state is to commite a mutation
然后state渲染vue组件

getters: need to compute or filter from derived state based on store state, 需要return

shopping cart shows that in a vue project, there is only one store that stores all the shared-data. Even if there are several store modules. Store modules are separated preventing complicated writing and understanding of massive shared-data. we can check getters object to prove it.

Remember: store is a single state tree! which means all state of our application is contained inside one big object.

In store, we cannot use the store variable，∵ store is not defined.
Each store modules handle the state related getters actions. But mutations can be defined in other store module.js.

Add "empty" function comes across some trouble. Since "mocking server data" cannot be fully the same as the server. When trying to empty shopping cart and restore the original data, there should be a whole new set of products which could not be polluted, but mocking the data cannot be satisfied. (But in this case, we can try another method, put cartProducts and Productslist leftovers together!)

Array Function:
    map, find, findIndex, reduce

in a vue project, can we just use css-loader, style-loader to resolve css? let's give it a try.
"vue-style-loader": "^2.0.5",


  CDN原理

  this week point:
    promise
    vue-vueRouter-vuex
    webpack
    es6


display: flex 兼容性
清除cookie一定要带着domain
query不行，用param试试

