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

