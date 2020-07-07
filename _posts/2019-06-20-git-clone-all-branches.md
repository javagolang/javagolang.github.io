---
layout:     post
title:     Basic git commands
date:       2019-07-16
author:     Datoucai
header-img: img/turtlrtitle3.jpg
catalog: true
tags:
    - git


---

> 龟龟是最可爱的猫




```bash
git clone URL
```

### git  clone URL通常只会克隆一个分支，那么如何clone所有分支呢？

```bash
git branch -v
* master 093df85 init commit

```

可以查看到只有一个分支

通过

```bash
git branch -a
```



则可以查看所有隐藏分支

```bash
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
  remotes/origin/testbranch

```

如果需要在某个分支上工作，需要

```bash
git checkout -b testbranch origin/testbranch
Branch testbranch set up to track remote branch testbranch from origin.
Switched to a new branch 'testbranch'
```

现在再查看

```bash
 git branch -v
  master     093df85 init commit
* testbranch 2bdf3c3 test
```

可以看到testbranch，且可以在该分支开发





### git push 出现  remote error:

```bash
remote: error: refusing to update checked out branch: refs/heads/dev
remote: error: By default, updating the current branch in a non-bare repository
remote: error: is denied, because it will make the index and work tree inconsistent
remote: error: with what you pushed, and will require 'git reset --hard' to match
remote: error: the work tree to HEAD.
remote: error:
remote: error: You can set 'receive.denyCurrentBranch' configuration variable to
remote: error: 'ignore' or 'warn' in the remote repository to allow pushing into
remote: error: its current branch; however, this is not recommended unless you
remote: error: arranged to update its work tree to match what you pushed in some
remote: error: other way.
remote: error:
remote: error: To squelch this message and still keep the default behaviour, set
remote: error: 'receive.denyCurrentBranch' configuration variable to 'refuse'.
To /media/zym/zym-usb/grayscale/
 ! [remote rejected] dev -> dev (branch is currently checked out)
error: failed to push some refs to '/media/zym/zym-usb/ggg/'
```



#### Solution:

```bash
git config receive.denyCurrentBranch ignore
```

### git 放弃工作区/暂存区/修改

1. 文件已修改，还没有add 使用``` git checkout -- fileA``` 可以撤销git在工作区的修改
2. 文件已经修改并且add进暂存区，分两步：先用 `git reset <文件名>` 撤销 `git add` 操作（此时更改仍留在工作区），再执行 `git checkout -- 文件名` 清除工作区的改动
3. 修改后，文件放入暂存区，且文件再次修改：分三步：先用 `git checkout -- 文件名` 撤销工作区的改动，再用 `git reset <文件名>` 撤销 `git add` 操作（此时更改仍留在工作区），最后执行 `git checkout -- 文件名` 清除工作区的改动

通过 git checkout -- 文件名 命令可以撤销文件在工作区的修改。
通过 git reset 文件名 命令可以撤销指定文件的 git add 操作，即这个文件在暂存区的修改。



### git clone with submodules

### git pull相关

git pull --rebase

#### git 想要撤销上一次拉取，可以通过reset HEAD实现

git reflog 查看记录

git reset --hard HEAD@{n} //返回一个特定的HEAD

```bash
git clone --recurse-submodules
```
