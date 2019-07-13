## git笔记自用 ~~markdown练习~~
#### 仓库创建的2种方法
##### 1.github创建后直接git clone到本地。  
##### 2.本地创建仓库后，关联到GitHub仓库。

```
git init
git remote add origin xxx.git //关联到远程
git push -u origin master //把本地库的所有内容推送到远程库上
```
由于新建的远程仓库是空的，所以要加上-u这个参数，等远程仓库里面有了内容之后，下次再从本地库上传内容的时候只需下面这样就可以了: 
`git push origin master`

---
##### 基本操作

```****
git status //查看状态
git clone <地址>
git add .
git add <file> //提交到暂存区
git commit -m “xxx” //暂存区提交到版本库
git commit -a -m ‘xxxx’ //把'已经跟踪过'的文件暂存起来一并提交，跳过git add步骤

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
情况一：commit后发现有遗漏
	   重新提交并合并替代上一次提交，两次整合为一次新的提交
如： git commit -m 'initial commit'
  	 git add <forgotten_file>
	 git commit --amend  //amend命令
	 
git checkout <file>  //拉取暂存区文件恢复到工作目录（丢弃工作区的改动,比较危险）
git reset HEAD  <file>  //拉取最近一次提交到版本库的文件到暂存区 （取消暂存，工作区不变）
```

---
##### 比较
```
git diff //不加参数即默认比较工作区与暂存区
git diff —staged //比较暂存区与最新本地版本库
```

---
##### 本地分支
```
git branch <newname> //创建分支，指向当前本地版本库
git branch -d <name> //删除分支
git branch -v //查看每一个分支的最后一次提交
git branch --merged //查看哪些分支已经合并到当前分支(然后就可以删除那个分支了)
git checkout -b <newname> //新建分支并切换到上面
git checkout <name> //切换当前分支(会改变本地内容)
git merge <name> //把分支xxx合并到当前分支（若2分支diverged，叫合并提交，自动创建基于2个父提交的新快照，并指向它）
//合并提交当对同一文件同一处有不同改动时，会冲突，需要用一些手段处理

git log 高级用法:
	git log --oneline --decorate
	--oneline 把每个提交压缩为一行，只显示id和第一行信息
	--decorate 显示指向提交的所有引用（分支、标签等）

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
git fetch origin
//查找 “origin” 是哪一个服务器，从中抓取本地没有的数据，并且更新本地数据库，移动 origin/master 指针指向新的、更新后的位置。

git push <远程主机名> <本地分支名> : <远程分支名> 
git push origin master //将本地主分支推到远程主分支
git push origin <local_branch> //创建远程分支， origin是远程仓库名


git push 
git checkout -b  xxx orgin/xxxx
git checkout master
git pull //抓取信息，更新本地数据库和本地工作区文件？
git tag 打标签//未细看
```

