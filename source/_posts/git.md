### git命令
git init 初始化
git status 状况
git add .添加
git rm -r --cached 要忽略的文件
git commit 将本地的变化提交到本地仓库文件夹 归档
git commit --amend -m [message]使用一次新的commit，替代上一次提交 如果代码没有任何新变化，则用来改写上一次commit的提交信息
git diff 可以用于对比当前状态和版本库中状态的变化
git log 可以查看提交日志
git reset --hard 版本  回归到指定版本
git push origin HEAD –force  执行完回滚版本后，在执行这个可以删除回滚版本之后的commit
git clone + git地址

git checkout -b dev origin/dev

---------------------------------------------------------------------
git stash // 保存当前工作进度，会把暂存区和工作区的改动保存起来
git stash save 'message...' // 可以添加一些注释
git stash list // 显示保存进度的列表。
git stash drop [stash_id] // 删除一个存储的进度。如果不指定stash_id，则默认删除最新的存储进度。
git stash clear // 删除所有存储的进度。

---------------------------------------------------------------------

### git提交顺序
```
	git init 初始化
	git status 状况
	git add .添加
	git commit -m '名称'将本地的变化提交到本地仓库文件夹 归档
	git remote rm origin // 删除远程仓库地址
	git remote add origin https://github.com/QSpinach/git-demo.git // 添加远程仓库地址
	git remote set-url origin https://github.com/QSpinach/git-demo.git // 更改远程仓库地址
	git push -u origin master // 强制push
	git pull origin master 把GitHub上的项目取下来
```

### 站点
	1、git branch gh-pages
	2、git checkout gh-pages  选择分支
	3、git push -u origin gh-pages

访问网址：qspinach.github.io/ + 项目名


### 合并项目：git merge syq-dev
一、
	1、从另一个版本中取回 git pull + 路径 （master）
二、
	1、分享版本库 git clone --bare
	** git push --set-upstream origin syq-dev 本地新建的syq-dev分支，提交需要与远程分支关联
	2、push到bare版本库中 git push + 版本库路径 master
	3、pull取回 git pull + 版本库路径 master

git clone -b 克隆指定分支

-------------------------------------------------------------------------------------------
### git 配置
git config --global user.name "xxxx"   设置用户名

git config --global user.email "xxxx"    设置邮箱

git config user.name     查看用户名

git config user.email    查看邮箱

git config --global user.name "xxxx" 修改用户名

git config --global user.email "xxxx@xxx.com" 修改邮箱

----------------------------------------------------------------------------
### git一些问题
git push 报错
error: src refspec master does not match any.
原因是本地仓库为空
解决办法是本地commit以下再提交

----------------------------------------------------------------------------
git 这个分支bug没改完切换到其他分支改bug，再切会来继续改bug

1、执行 $ git stash 命令，将当前分支修改的内容 stash 起来
2、执行 $ git stash list 命令，查看 stash 列表，会看到已经刚才的修改已存储
3、执行 $ git status 命令，显示没有东西需要提交，这个时候你就可以切换到其他分支了
4、执行 $ git branch | $ git checkout 切换分支
5、修复完紧急的 Bug 后，就可以切回之前的分支，进行未完成的内容
6、执行 $ git stash list 命令，查看 stash 列表
7、执行 $ git stash apply stash@{0} 命令，恢复 id 为 4240c0c 的 stash 的内容
8、执行 $ git stash drop stash@{0} 命令，删除 stash 列表中已经恢复的 id 为 4240c0c 的 stash 记录
