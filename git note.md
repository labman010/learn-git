## git笔记自用 ~~markdown练习~~
#### 仓库创建的2种方法
##### 1.github创建后直接git clone到本地。  
##### 2.本地创建仓库后，关联到GitHub仓库。

```
git init
git remote add origin xxx.git //关联到远程
git push -u origin master //把本地库的所有内容推送到远程库上
```
由于新建的远程仓库是空的，所以要加上-u这个参数，等远程仓库里面有了内容之后，下次再从本地库上传内容的时候只需下面这样就可以了: 
`git push origin master`

#### git config ####

`git config --global credential.helper store		//永久保存密码？`

`/etc/gitconfig    git config 时用 --system     //本机设置`

`~/.gitconfig   git config 时用 --global        //本用户设置`

`工作目录.git/config       直接git config	     //本目录全用户本机设置`





---
##### 基本操作

```****
git status //查看状态
git clone <地址>
git add .
git add <file> //提交到暂存区
git commit -m “xxx” //暂存区提交到版本库
git commit -a -m ‘xxxx’ //把'已经跟踪过'的文件暂存起来一并提交，跳过git add步骤

git log 会按提交时间列出所有的更新。列出每个提交的 SHA-1 校验和、作者的名字和电子邮件地址、提交时间以及提交说明。
```
git add 可以用它开始跟踪新文件，或者把已跟踪的文件放到暂存区，还能用于合并时把有冲突的文件标记为已解决状态等。  

---
##### 删除与改名
```
情况一：正常删除
rm  //字面意思，实际上是从工作区移除文件，但暂存区依然存在
git rm <file> //移除暂存区文件，并提交(git就不会继续跟踪了)也同时移除了工作区文件

情况二：想把文件从 Git 仓库中删除（亦即从暂存区域移除），
但仍然希望保留在当前工作目录中。 
换句话说，你想让文件保留在磁盘，但是并不想让 Git 继续跟踪。
git rm --cached

名字相关：
git rm log/\*.log  此命令删除 log/ 目录下扩展名为 .log 的所有文件

改名：
git mv <file_from> <file_to> //相当于：
  mv <file_from> <file_to> 
  git rm <file_from>
  git add <file_to>
  这三条命令

```

---

##### 恢复与撤销
```
~~commit后发现有遗漏
	   重新提交并合并替代上一次提交，两次整合为一次新的提交
如： git commit -m 'initial commit'
  	 git add <forgotten_file>
	 git commit --amend  //amend命令
	 
~~ git checkout <file>  //拉取暂存区文件恢复到工作目录（丢弃工作区的改动,比较危险）
	git checkout <hash> <<file>  //还原特定版本的文件
~~ git reset HEAD  <file>  //拉取最近一次提交到版本库的文件到暂存区 （取消暂存，工作区不变）

～～进度保存
#在工作正常进行时，突然需要切换到其他分支上处理一些东西
#这时如果直接切换，那么工作区的改动也会随之跟随到另一个分支
#如果是add然后再commit一下，有感觉麻烦或者是并不合适。
#只想将当前状态保存下来，git stash 是一个非常合适命令
git stash save '这是一条注释'  //保存
//像栈一样可以多次执行的
git stash pop //恢复最近的一个进度到工作区，工作区和暂存区的改动都恢复到工作区。
git stash pop --index  //会恢复最近的一个进度到到工作区和暂存区（从哪来回哪去）
pop命令后都会删除进度，除非apply

https://blog.csdn.net/daguanjia11/article/details/73810577

～～合并冲突解决
git merge --abort 
#仅在合并后导致冲突时才使用，
#重建合并前的状态，但未commit的内容不能恢复

~~ git pull 撤销误操作
## 把远程仓库的合并到本地分支，扰乱了
git reflog  //命令查看历史变更记录
git reset --hard HEAD@{n} 或 git reset --hard 40a9a83  //回退

~~ 撤销 amend
git reset --hard HEAD@{1}

https://juejin.im/post/5b5ab8136fb9a04f834659ba
...未完待续

```

---
##### 比较
```
git diff //不加参数即默认比较工作区与暂存区
git diff —staged //比较暂存区与最新本地版本库

git diff <commit1> <commit2> //比较两个commit id
```

---
##### 本地分支
```

git branch  //查看本地分支
git branch <newname> //创建分支，指向当前本地版本库
git branch -a //查看远程分支
git branch -d <name> //删除分支（比如有2个分支指向同一位置）
git branch -v //查看每一个分支的最后一次提交
git branch -vv //在-v基础上增加查看每个分支的跟踪分支（上游分支）
git branch --merged //查看哪些分支已经合并到当前分支(然后就可以删除那个分支了)
git checkout -b <newname> //新建分支并切换到上面
git checkout <name> //切换当前分支(会改变本地内容)
git merge <name> //把分支xxx合并到当前分支（若2分支diverged，叫合并提交，自动创建基于2个父提交的新快照，并指向它）
//合并提交使用两个分支的末端所指的快照以及这两个分支的工作祖先，做一个简单的三方合并。
//合并提交当对同一文件同一处有不同改动时，会冲突，需要用一些手段处理。

git log 高级用法:
	git log --oneline --decorate
	--oneline 把每个提交压缩为一行，只显示id和第一行信息
	--decorate 显示指向提交的所有引用（分支、标签等）
git log --oneline --decorate --graph --all 显示分支图表
git log --graph --decorate --oneline --simplify-by-decoration --all  

```
---
##### tag
```
两种标签：轻量标签、附注标签
git tag -a v1.4 -m 'my version 1.4'  //创建附注标签
git tag v1.4  //创建轻量标签
git show  //查看标签信息和对应提交信息
git tag -l 'v1.5.2*'  //特定模式查找标签

git tag -a <tagname> <部分校验和>  //后期打标签

默认git push 命令并不会传送标签到远程仓库服务器上。 
必须显式地推送标签到共享服务器上，像共享远程分支一样.
你可以运行 git push origin [tagname]
git push origin --tags //把不在远程仓库服务器上的标签全部传送

git tag -d <tagname>  删除轻量标签
git push <remote>:refs/tags/<tagname> //本地删除后更新远程仓库

git别名：git config --global alias.st status
//等

```
---
##### rebase 变基
```
git rebase变基，确保分支串行整洁
在dev1与master为两个分支的时候，不使用merge
git checkout dev1
git rebase master
然后git checkout master再git merge dev1
//最后两个分支都在最头上。

rebase高级用法：“重放”
如：git rebase --onto master server client
取出 client 分支，找出处于 client 分支和 server 分支的共同祖先之后的修改，
然后把它们在 master 分支上重放一遍

常用：git pull --rebase  //本地有commit没有push，pull下来别人的新提交，本地commit的parent接到它后面，继续本地修改

变基的风险与处理
```

---
##### 远程仓库
```
git remote  查看已配置的远程仓库服务器
git remote -v

git remote add <shortname> <url> 添加一个新的远程Git仓库，同时指定一个你可以轻松引用的简写.
如果你想拉取 Paul 的仓库中有但你没有的信息，
可以运行 git fetch pb

git push 生效条件：
当你和其他人在同一时间克隆，他们先推送到上游然后你再推送到上游，
你的推送就会毫无疑问地被拒绝。 
你必须先将他们的工作拉取下来并将其合并进你的工作后才能推送。 

```

---
##### 远程分支
```
远程仓库origin，远端分支master，本地分支master

git remote show origin //！！查看远程分支和本地分支的对应关系

git fetch  //将某个远程主机的更新，全部取回本地

git fetch origin
//查找 “origin” 是哪一个服务器，从中抓取本地没有的数据，并且更新本地数据库，移动 origin/master 指针指向新的、更新后的位置。
//结果是本地———远端分叉

先git fetch --all 后 git branch -vv
//用于要统计每个服务器分支最新的领先与落后数字

git push <远程主机名> <本地分支名> : <远程分支名> 
git pull <远程主机名> <远程分支名> : <本地分支名>//注意！ 
如git push origin dev:dev 
//推送本地的dev分支到远程origin的dev分支(远程没有会自动创建)
//同 git push origin <branchName>

git push origin <branchName>
git push -u origin <branchName>//上基础上设置默认主机为origin

git push --set-upstream origin  xxx
//将本地的xxx分支推送到origin主机,之后就改变了默认的远程关联仓库

git push 
git checkout -b  xxx orgin/xxx //本地新建分支并拉取远程分支到此

git pull //抓取信息，更新本地数据库和本地工作区文件
git pull //基本是一个git fetch紧接着一个git merge 命令
git tag 打标签//未细看
```

```
分支的删除

git branch -d <local_branch> //删除本地分支

git push origin :<branchName> //push空分支
等同于
git push origin -d <branchName>
删除指定的远程分支


```
---
#### repo命令和原理
```c
repo init
repo sync
repo sync -c    //直接同步当前分支的全部东西
repo forall -c git checkout speed/release/WL_190904    //切换全部分支为xxx
repo start branch –all xxxx  //切换全分支为xxx  ？？？
```

```
git push origin localbranch:refs/for/******
```

 

