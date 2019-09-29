## 多人项目git典型用例 

##### 基本操作

```
git status //查看状态
git clone <地址>

```
git add 可

---

##### 同步远程仓库分支
[简书4个例子](https://www.jianshu.com/p/811b07b129e8)

```
问题一：本地新建分支，push时报错
（1）git push origin xxx  
	 把本地的xxx分支推向指定的分支xxx(没有就自动新建)。
（2）关联远程分支。
	  git push --set-upstream origin xxx
	  关联远程的分支这样下一次push就不用(1)直接git push

```

---

#####  使用git pull文件时和本地文件冲突怎么办

```
git stash  //先将本地修改存储起来
git pull   //暂存了本地修改之后，就可以pull了
git stash pop stash@{0}   //还原暂存的内容

git mergetool    //解决文件中冲突的的部分
```



##### 提交commit后，或者已经push了，发现需要修改

```
直接修改
git add .
git commit --amend 
git push origin  dipper8/master:refs/for/dipper8/master

需要大量修改，push的东西就不要脸，直接退回上一次commit重新写
$ git reset --soft commit_id  # 回退到上一个提交的节点 代码还是原来你修改的
$ git reset –-hard commit_id # 回退到上一个commit节点， 代码也发生了改变，变成上一次的


git 让单个文件回退到指定版本
git checkout <hash> <filename>
```




git revert  后 撤销某个提交，并且把这个操作作为新的提交

git rebase -i

git回退远程提交并amend修改https://blog.csdn.net/zsago/article/details/73618279

