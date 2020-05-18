---
title: Git拉取远程最新代码，并与当前分支合并
comments: true
categories:
  - Git
tags:
  - Git
abbrlink: e235697f
date: 2019-04-03 21:30:41
---

在团队开发中，git的使用已经很常见了，在多人协同开发中，我们经常会遇到这样的问题：A在本地开发完成后，将代码推送到远程，这时候B的本地代码的版本就低于远程代码的版本，这时候B该如何从远程拉取最新的代码，并与自己的本地代码合并呢？ 具体步骤如下：

#### 查看远程仓库:

```
git remote -v
```

#### 看到远程有一个叫origin的仓库，我们可以使用如下命令从origin远程仓库获取最新版本的代码

```
git fetch origin master:temp
```

- 上面代码的意思是：从远程的origin仓库的master分支下载到本地master并新建一个temp分支

- 注意：不建议使用pull拉取最新代码，因为pull拉取下来后会自动和本地分支合并

  获取最新版本  有两种  拉取 和 获取 pull 和 fetch

> git  pull     从远程拉取最新版本 到本地  自动合并 merge `git pull origin master`
>
> git  fetch   从远程获取最新版本 到本地   不会自动合并 merge    `git fetch  origin master`       `git log  -p master ../origin/master `    `git merge orgin/master`
>
> 实际使用中  使用git fetch 更安全    在merge之前可以看清楚 更新情况  再决定是否合并

#### 查看temp分支与本地原有分支的不同

```
git diff temp
```

#### 将temp分支和本地的master分支合并

```
git merge temp
```

#### 删除temp分支

```
git branch -D temp
```

