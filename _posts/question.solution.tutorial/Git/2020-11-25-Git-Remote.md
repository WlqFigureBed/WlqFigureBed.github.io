---
layout:     post
title:      "【Git Three】 Git 浅析远程协作"
subtitle:   "How To Use Git For Remote Collaboration"
date:       2020-11-23 22:15:00
author:     "HapppyTsing"
catalog: false
header-style: text
tags:
  - Git
---

> 本篇主要讲解Git本地和远程仓库交互协作。

# git remote

```shell
git remote -v                                # 可以查看该本地仓库和哪个远程仓库连接，若为空，则进行连接：
git remote add origin git@github~.git        # origin 是 Git 默认的远程仓库名
git remote rename origin <new originname>    # 更新 origin 的名字为 newname
git remote remove origin                     # 删除 origin
```

查看本地分支与远程分支的关联：`git branch -vv`

# git clone

克隆一个git项目：

```shell
git clone git@github~.git 
```

# git push

将本地仓库的提交推送到远程仓库

```shell
git push                       # 推送默认分支(当前分支)

git push origin master         
# 推送指定分支 master 到远程仓库的 master 分支，相当于 git push origin master:master

git push origin localbranch:remotebranch 
# 推送指定分支 localbranch 到远程仓库的 remotebranch 分支,如果remotebranch不存在，则创建


git push origin :remotebranch  # 推送“空分支”到远程仓库的 remotebranch 分支,即删除远程仓库中的分支 remotebranch
git push --delete remotebranch # 删除远程分支，效果同上

git push origin --tag          # 推送所有tag
git push origin --all          # 推送所有分支和tag
```

**Params**

- --tag：推送所有tag
- --all：推送所有分支和tag
- --force：强制推送，用本地分支覆盖远程分支
- --delete：删除远程分支

**zsh shortcut**：`gp`

# git fetch

先说说一个命令：`git branch -r`，该命令显示所有远程分支。因为分布式的关系，这里的远程分支，其实是本地仓库中对应远程仓库分支的本地映射，并不是指实际服务器上的分支，是通过 git fetch 等来同步的。 

因此，`git fetch`的作用就是拉取远程仓库中所有分支的更新，并同步到本地仓库中的远程分支，即origin/xxx。

# git pull

- 简单说：拉取当前分支对应的远程仓库中的更新，并合并到当前分支。

- 复杂说：拉取默认远程仓库中与当前分支建立了同步流的分支（这个分支通常是和当前分支同名），并更新到当前分支。通常一个仓库只有一个远程仓库配置，别名叫做 origin。

实际上，`git pull` 包含多个操作： 

1. `git fetch`：拉取远程仓库中所有分支的更新，并同步到本地仓库中的远程分支，即origin/xxxx 分支
2. `git merge`：将与当前分支建立了更新流的远程分支合并（merge）到当前分支

```shell
git pull origin                # 拉取远程仓库 origin，如果有多个远程仓库时，需要显式的指定要拉取的远程仓库是比较安全的
git pull origin <branch name>  # 拉取远程仓库 origin 的指定分支
```

**zsh shortcut**：`gl`

# References

