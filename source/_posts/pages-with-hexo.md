---
title: Pages with Hexo
date: 2018-03-17 10:54:46
tags: [hexo, github pages] 
---

This is my very first post about how to build github pages with Hexo.
Below are some issue that I encounterd and settled when I was setting up. 

## First push

After "git clone" the repository from origin to local, I followed the steps that Hexo tells to complete some basic settings, and ran "hexo s", things was fine. However when trying to push them to origin master, I got this: 

"fatal: unable to access 'https://github.com/DanaKuang/baymax.github.io.git/': The requested URL returned error: 403". 

"403" means there is no permission for me to push into the repository. So here is the solution:

``` bash
$ cd blog
$ vim .git/config
```

```
[remote "baymax-blog"]
        url = https://github.com/XXaccountXX/XXrepositoryXX.github.io.git

#change the above 'url' to the below

[remote "baymax-blog"]
        url = https://XXaccountXX@github.com/XXaccountXX/baymax.github.io.git       
```

Then "git push" again, enter the password of repository, and done！

"hexo deploy" can also help to push, but it needs to be installed first.

``` bash
$ npm install hexo-deployer-git --save
```

## Page build failed: Unknown tag error

## layout disorder

正式部署之前需要改下root 不再是 / 而是 域名下面的第一路径 /baymax.github.io/

可是图片路径仍然不对.

然后把 theme config下面# Images Settings 的img改成相对路径，就好了。去掉前面的/

这样本地也是好的。并且本地的服务搭建在http://localhost:4000/baymax.github.io/地址，而不是localhost:4000

但是还有一个小问题啊，就是点进去每个页面的avatar路径还是不对。。




