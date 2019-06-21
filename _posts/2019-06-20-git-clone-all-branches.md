```bash
git clone URL
```

通常只会克隆一个分支，那么如何clone所有分支呢？

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