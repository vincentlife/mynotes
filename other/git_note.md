# Basic Knowledge
本地仓库由 git 维护的三棵树组成。工作目录，持有实际文件； 暂存区（Index,或者stage），像个缓存区域，临时保存改动；最后是HEAD，指向最后一次提交的结果。
所以，git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行git commit就可以一次性把暂存区的所有修改提交到分支。
## origin
origin指向远端代码库，是一个名字。origin指向的是repository。可以通过git remote add name url 添加新的

## 密码缓存
git config --global credential.helper cache
//Set the cache to timeout after 1 hour (setting is in seconds
git config --global credential.helper 'cache --timeout=3600'


# 创建
## config
* git config -l 
* git config --global user.name "You Name"
* git config --global user.email yourmail@server.com
## 

## clone
git clone <版本库的网址> <本地目录名> 该命令会在本地主机生成一个目录，与远程主机的版本库同名。如果要指定不同的目录名，可以将目录名作为git clone命令的第二个参数。

## checkout
* 取远程分支并分化一个新分支： git checkout -b mylocalbranch origin/myremotebranch

## remote
* git remote -v # 查看远程服务器地址和仓库名称
* git remote show origin # 查看远程服务器仓库状态
* git remote add origin https://github.com/user/repo.git 添加远程仓库地址
* git remote set-url origin https://youruser:password@github.com/user/repo.git 设置远程仓库地址(用于修改远程仓库地址) 
* git remote rm <repository> # 删除远程仓库
* git remote set-head origin master # 设置远程仓库的HEAD指向master分支
也可以命令设置跟踪远程库和本地库

## branch

# 提交
## add
* git add <file> # 将工作文件修改提交到本地暂存区
* git add . # 将所有修改过的工作文件提交暂存区

## commit
* git commit -m "commit message"

## rm
* git rm <file> # 从版本库中删除文件
* git rm <file> --cached # 从版本库中删除文件，但不删除文件
* 在被 git 管理的目录中删除文件时，可以选择如下两种方式来记录删除动作：rm + git commit -am "abc" 。git rm + git commit -m "abc"

## push
* git push 如果当前分支只有一个远程分支，那么主机名都可以省略
* git push origin  如果当前分支与远程分支存在追踪关系，则本地分支和远程分支都可以省略，将当前分支推送到origin主机的对应分支。
* git push origin master # 将本地主分支推到远程主分支
* git push -u origin master # 将本地主分支推到远程(如无远程主分支则创建，用于初始化远程仓库)
* git push origin <local_branch> # 创建远程分支， origin是远程仓库名
* git push origin <local_branch>:<remote_branch> # 创建远程分支
* git push origin :<remote_branch> #先删除本地分支(git br -d <branch>)，然后再push删除远程分支

## pull

# 恢复
## log
git log file 

## diff
* git diff 不加参数即默认比较工作区与暂存区
* git diff [<commit-id>] [<commit-id>] 比较两个commit-id之间的差异

## reset
* git reset file # 从暂存区恢复到工作文件
* git reset commitid file
* git reset -- . # 从暂存区恢复到工作文件
* git reset --hard # 恢复最近一次提交过的状态，即放弃上次提交后的所有本次修改

## revert
git revert 是生成一个新的提交来撤销某次提交，此次提交之前的commit都会被保留
git reset 是回到某次提交，提交及之前的commit都会被保留，但是此次之后的修改都会被退回到暂存区

## stash
可以获取你工作目录的中间状态——也就是你修改过的被追踪的文件和暂存的变更——并将它保存到一个未完结变更的堆栈中，随时可以重新应用。
* git stash
* git stash list
* git stash apply
* git stash pop 从Git栈中读取最近一次保存的内容，恢复工作区的相关内容。
* git stash clear 清空stash列表


# 常用操作
## 合并远程分支
假设这两个分支是a和b，那么fetch a和b，checkout a，将b merge到a，push a到远端。这样做，将b和a合到了一起，并且更新了本地和远端的a。
pycharm中
checkout到本地的master上，在master上去merge dev

## gitignore
已经开始进行版本管理的文件不会受到gitignore的影响
/dir/ 忽略当前目录下的dir文件夹
dir/ 忽略所有的dir文件夹
*.zip 过滤所有.zip文件

gitignore还可以指定要将哪些文件添加到版本管理中：
!*.zip
!/dir/one.txt