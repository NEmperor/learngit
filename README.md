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
