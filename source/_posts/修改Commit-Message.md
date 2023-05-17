---
title: 修改Commit Message
date: 2020-11-17 15:33:28
tags:
  - git
category: Git
author: Xavier
---
# 修改Commit Message

## 修改上一条提交的 commit message

```
git commit --ammend
```

## 修改之前提交的 commit message

首先，我们需要使用 `git rebase -i`, `git rebase -i` 提供一个参数，指明你想要修改的提交的父提交（-i 是--interactive的缩写）

例如：修改最近三次提交，事实上所指的是四次提交之前，即你想修改的提交的父提交

```
git rebase -i HEAD~3
```

接着会显示如下界面

```
pick ef3f7de158 refs #16605[Fix]Not all approver is shown
pick e0e5e8f595 refs #17605 change goalesce field to user id
pick 3e0cfc1536 refs #17605 change user id to immutable and required_true_can_update

# Rebase 9e993debaf..3e0cfc1536 onto 9e993debaf (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
```

选择你要修改的那一条commit，把 pick 改为 edit，然后保存退出

接着，就可以修改选定commit的commit message了

```
git commit --ammend
```

修改好之后，运行 `git rebase --continue`

然后，就没有然后了~~