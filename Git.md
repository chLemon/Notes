# Git

```
git安装
git设置：
git config --global user.name "Your Name"
git config --global user.email "email@aa.com"
版本库/仓库/repository
git init
把一个目录变成git管理的仓库

git add 文件
把文件添加到仓库

git commit - m "message"
把文件提交到仓库

git status
查看仓库状态

git diff 文件
查看修改

git log
查看提交日志
可选参数：
-pretty=oneline

git reset --hard HEAD^
版本回退
HEAD是当前版本
HEAD^上个版本
HEAD~100，上100个版本
或者输入commit id，只需要输入几位能搜索到就行

git reflog
记录每一次命令，可以查看commit id

stage/index：暂存区，add就是把文件加入暂存区
commit是把暂存区提交到分支上

git checkout -- file
用版本库的版本替换工作区。
丢弃工作区的修改，让这个文件回到最近一次add或commit时的状态
或者是恢复工作区文件

git reset HEAD file
撤销掉暂存区的修改

git rm file
git commit
从版本库删除掉某个文件

https://www.liaoxuefeng.com/wiki/896043488029600/896954117292416
ssh配置问题

```

