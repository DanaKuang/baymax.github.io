---
title: My First GitHub Pages
date: 2018-03-17 10:54:46
tags:  
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

Then "git push" again. After entering the password of repository, done！

"hexo deploy" can also help to push, but it needs to be installed first.

``` bash
$ npm install hexo-deployer-git --save
```

## Page build failed: Unknown tag error



