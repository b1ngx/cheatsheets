Git


##### 撤销上次 commit

```
git reset --soft HEAD^
```

HEAD^：上一个版本，也可以写成 HEAD~1， HEAD~2 撤销 2 次 commit
--soft：不删除工作区改动，撤销 commit , 不撤销 git add .
--hard：删除工作区改动，回到上一次 commmit 状态.

##### 修改 commit message

```
git commit --amend
```

##### 删除远程已经删除的分支

```
git remote prune origin
```
