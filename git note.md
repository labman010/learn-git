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

-
```****
git status //查看状态
git clone <地址>
git add .
git add <file> //提交到暂存区
git rm <file> //移除暂存区文件，并提交(git就不会继续跟踪了)也同时移除了工作区文件
git mv  <file1> <file2> //重命名
git commit -m “xxx” //暂存区提交到版本库
git commit -a -m ‘xxxx’ //把'已经跟踪过'的文件暂存起来一并提交，跳过git add步骤
```
##### 恢复操作
```
git checkout <file>  //拉取暂存区文件恢复到工作目录（丢弃工作区的改动,比较危险）
git reset HEAD  <file>  //拉取最近一次提交到版本库的文件到暂存区 （取消暂存，工作区不变）
```
##### 比较
```
git diff //不加参数即默认比较工作区与暂存区
git diff —staged //比较暂存区与最新本地版本库
```
##### 远程仓库与分支
```
git branch <newname> //创建分支，指向当前本地版本库
git checkout -b <newname> //新建分支并切换到上面
git checkout <name> //切换当前分支(会改变本地内容)

git remote -v //查看远程仓库
git push
git checkout -b  xxx orgin/xxxx
git checkout master
git pull
git fetch
git tag 打标签//未细看
```

