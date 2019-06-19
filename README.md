## git remote add origin https://github.com/NEmperor/learngit.git
### 将 origin 的值设置成 https://github.com/NEmperor/learngit.git

.git/config文件 添加
```
[remote "origin"]
	url = https://github.com/NEmperor/learngit.git
	fetch = +refs/heads/*:refs/remotes/origin/*
```
## git checkout -b test1
### 创建一个新的分支test1
* 添加文件和内容
* git add .
* git commit -m 'first commit'

执行 git push 报错
```
fatal: The current branch test1 has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin test1
```
执行 git push origin 也报错
```
fatal: The current branch test1 has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin test1
```
按照提示执行 git push --set-upstream origin test1，输入账号和密码，成功，完成了两件事
1. 文件成功提交到git仓库的test1分支
2. .git/config 添加了一个配置选项
```
[branch "test1"]
	remote = origin
	merge = refs/heads/test1
```
以后再向远程分支test1提交时，执行 git push ，输入用户名和密码就可以

## git rm --cache <file>  删除暂存区的文件
* 当暂存区的文件和工作区的文件不一致时，需要加参数 -f
* 暂存区只保留最新add 提交的内容，git commit 后，暂存区提交到历史区，暂存区的内容依然保持不变。
* 目前能修改的暂存区的内容的指令：
    1. git rm --cache <file> 操作删除 暂存区的文件
    2. git add <file> 更新暂存区的文件
## git checkout <file> 将暂存区的文件覆盖工作区的文件

# 代码回滚
* git reset HEAD .  清空暂存区 ，使 暂存区和历史区最近一次提交历史相同
* git checkout . 把暂存区内容回滚到工作区，一旦回滚，工作区无法恢复.(清除工作区没有add的修改)
* git reset --hard 版本号 在历史区回退到某一个版本，强制把工作区和暂存区变成回退后的版本

## stash

将工作和暂存区的状态存储起来以备将来使用，并将当前工作区和暂存区重置为最近一次提交后的状态
1. 修改了一个问文件的内容，此时是modified
```
 modified:   README.md
```
2. 此时不能切换到其他分支，执行 `git stash`,变回到和上次提交的内容相同，状态变成clean
3. 执行`git status`
```
nothing to commit, working tree clean
```
4. 查看stash列表 `git stash list`,在master分支上有一个stash
```
stash@{0}: WIP on master: 720f56b stash
```
5. 可以切换到其他分支test1进行操作，在test1分支也建立一个stash
6. 切回到master分支，此时master分支状态是 clean
7. 执行 git stash list
```
stash@{0}: WIP on test1: 1e31fc8 stash
stash@{1}: WIP on master: 720f56b stash
```
8. 执行 `git stash pop stash@{1}`,master变回到切回之前，准确的说是执行`git stash`之前的内容
* 执行 `git stash pop stash@{1}`时，状态必须是clean
* 如果在master分支执行 `git stash pop stash@{1}`,stash@{1}属于master分支,会消除stash@{1},
* 如果在master分支执行 `git stash apply stash@{1}`不会会消除stash@{1}
* 如果在master分支clean的状态下，执行`git stash pop stash@{0}`,stash@{0}不会消失，因为stash@{0}属于test1分支,这种使用场景一般不会出现

### 删除stash操作
* 下面的两种的方法都可以在当前分支上删除其他分支的stash
```
git stash drop stash@{1} # 删除指定储藏
git stash clear #  删除所有储藏
```
