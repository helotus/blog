## mac
>cd ~/.ssh
>ssh-keygen -t rsa -C "xxx@xx.com"

创建 ssh-key
ssh -keygen   copy到ssh

git config --global user.name ""
git config --global user.email ""


## Git分支：

查看当前分支：git branch
查看全部分支：git branch -a
创建分支：git branch <name>
切换分支：git checkout <name>
创建+切换分支：git checkout -b <name>
修改本地分支：git branch -m new_branch wchar_support
丢弃工作区的修改：git checkout . /git checkout -- file
暂存文件：git add .
删除文件：git rm file

# 撤消操作 修改最后一次提交 说明
git commit -m 'initial commit'
git add forgotten_file
git commit --amend

# 合并特定的commit到分支
dev: git cherry-pick 62ecee  

## 代码回退
# 线上代码回滚 git reset
--soft 回退后a分支修改的代码被保留并标记为add的状态（git status 是绿色的状态）
--mixed 重置索引，但不重置工作树，更改后的文件标记为未提交（add）的状态。默认操作。
--hard 重置索引和工作树，并且a分支修改的所有文件和中间的提交，没提交的代码都被丢弃了。
--merge 和--hard类似，只不过如果在执行reset命令之前你有改动一些文件并且未提交，merge会保留你的这些修改，hard则不会。【注：如果你的这些修改add过或commit过，merge和hard都将删除你的提交】
--keep 和--hard类似，执行reset之前改动文件如果是a分支修改了的，会提示你修改了相同的文件，不能合并。如果不是a分支修改的文件，会移除缓存区。git status还是可以看到保持了这些修改。

本地代码库版本回退：git reset HEAD~3 最近3次回退
查看提交,分支历史：git log  / git log --pretty==oneline / git log --graph
指向当前版本号：git reset --hard HEAD^
查看每次命令：git reflog 
合并指定分支到当前分支：git merge dev
普通模式合并分支：git merge --no-ff -m "merge with no-ff" dev
修复bug（创建分支修复，合并，删除）--> 暂时储存当前任务：git stash -> git stash list -> git stash pop(恢复并删除stash) -> git stash list

查看远程仓库信息：git remote -v
在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
抓取内容解决冲突再本地推送分支：git branch --set-upstream dev origin/dev -> git push origin dev


## 标签
创建标签(默认HEAD)：git tag v1.0 /git tag v0.9 commit id -> git tag
标签说明：git tag -a v0.1 -m "version 0.1 released" 3628164 -> git show <tagname>
推送一个本地标签：git push origin <tagname>
推送全部未推送过的本地标签：git push origin --tags
删除一个本地标签：git tag -d <tagname>
删除一个远程标签：git push origin :refs/tags/<tagname>

## 代码合并
feature-branch:  git pull --rebase origin dev 用于在feature branch上同步最新的dev代码
git rebase master dev //合并分支
git rebase dev master
git rebase --continue
git rebase --quit

# 合并线上分支代码到本地
git pull origin release

dev: git merge --no-ff feature-branch 用于把feature branch合并到dev
dev: git push

git push origin release --force 如果远程主机的版本比本地版本更新，推送时Git会报错，要求先在本地做git pull合并差异，然后再推送到远程主机。这时，如果你一定要推送，可以使用--force选项。


## 删除
删除一个本地标签：git tag -d <tagname>
删除一个远程标签：git push origin :refs/tags/<tagname>

删除本地分支：git branch -d <name>
丢弃没有被合并的本地分支，强行删除：git branch -D <name>
删除远程分支：git push origin --delete :<name>
删除远程分支：git push --delete origin :<name> 

