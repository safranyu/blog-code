---
title: git分支的创建与使用
comments: true
categories:
  - Git
tags:
  - Git
abbrlink: adk7e5ef
date: 2020-04-22 19:02:06
---

在此记录下命令：

创建命令：
git branch 分支名

切换分支：
git checkout 分支名

创建并切换分支
git checkout -b 分支名

删除分支
git branch -d 分支名
ps：如果需要删除的分支为合并到主分支git报错，此时可以用-D 大写的d来删除

![](http://img.cdn.vmccc.cn/7269362-bf03355a365c8e68.png)

合并分支：

git merge 分支名 （将分支名合并到当前分支！ps:注意是当前分支）
注意：若指定分支与当前分支没有冲突，则执行快速合并。若存在冲突则快速合并失败 需要查看冲突的文件并手动解决冲突后在提交文件

git 后悔药

重置到上一次的提交

git reset --hard HEAD^

重置到上两次的提交

git reset --hard HEAD^^

git log 查看日志

重置到某一个分支

git reset --hard commitId

重点：后悔药的后悔药

git reflog

查看所有的操作日志,在此可以查到最后一次的的commitid，然后就可以找 最新的commitid使用

git reset --hard

最新的commitid即可

git日志以类图形化显示

git log --graph --decorate --oneline --all


## 快捷语法

1、`ggpush` 提交

2.`gcc test` 创建分支