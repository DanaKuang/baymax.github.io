---
title: 关于git
date: 2018-03-23 09:59:23
tags:
---

碰到要更改域名，连带把远程仓库的名字也改了，怎么做呢？

第一种：
vim .git/config
把[remote "origin"]下面的url
    url = git@git.XXX.cn:仓库名.git 改成要变的
这样，即便用了source-tree，也可以发现source-tree里面的repository也变了。

第二种：
git remote set-url origin git@git.XXX.cn:仓库名.git

需要注意的而是，如果用了sourceTree这样的IDE，仅仅在它的配置文件里面改repository地址，是不会导致.git/config里面的origin也变化的。

变基：git rebase

回退到某个版本：

撤销commit

暂存

git merge