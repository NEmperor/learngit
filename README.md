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
* git reset HEAD .  清空暂存区 ，使 暂存区和历史区相同
* git checkout <file> 把暂存区内容回滚到工作区，一旦回滚，工作区无法恢复
* git reset --hard 版本号 在历史区回退到某一个版本，强制把工作区和暂存区变成回退后的版本

## 回滚测试1