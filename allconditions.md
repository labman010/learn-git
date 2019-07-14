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