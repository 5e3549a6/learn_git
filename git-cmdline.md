## 1. Git 常用命令

>   出处：[Git常用命令速查表（收藏大全） ](http://www.sohu.com/a/251952125_663371)

>   作者：郑未老师

**Git 名词：**

-   master: 默认开发分支
-   origin: 默认远程版本库
-   Index / Stage：暂存区
-   Workspace：工作区
-   Repository：仓库区（或本地仓库）
-   Remote：远程仓库

### 1.1. Git 初始化

```shell
# 当前目录初始化一个 git 代码库
git init

# 新建目录，并初始化为 git 代码库
git init <project-name>

# 下载一个 git 项目
git clone <git_url>
```

### 1.2. Git 配置

git 配置文件为 `.gitconfig`，如果放在项目目录，则为项目的配置；如果放在用户主目录，如 `/home/ubuntu/`，则为全局配置.

```shell
# 显示当前的 git 配置
git config --list 

# 编辑 git 配置文件
git config -e [--global]

# 设置提交代码时的用户信息
git config [--global] user.name "[name]"
git config [--global] user.email "[email address]"
```

### 1.3. Git 文件增删改

```shell
# 查看状态
git status 

# 查看变更内容
git diff 

# 添加指定文件到暂存区
git add <file1> <file2> ...

# 添加指定目录到暂存区，包括子目录
git add <dir>

# 添加当前目录的所有文件到暂存区
git add -

# 添加每个变化前，都会要求确认
# 如果一个文件有多出变化，可以实现分次提交
git add -p 

# 删除工作区文件，并将该次删除放入暂存区
git rm <file1> <file2> ...

# 停止追踪指定文件，但文件会保留在工作区
git rm --cached <file>

# 文件改名，并放入暂存区
git mv <file> <file-rename>
```

### 1.4. Git 代码提交

```shell
# 提交暂存区到仓库区
git commit -m <message>

# 提交暂存区的指定文件到仓库区
git commit <file1> <file2> ... -m <message>

# 提交工作区自上次 commit 之后的变化，直接到仓库区
git commit -a

# 提交是显示全部 diff 信息
git commit -v 

# 使用一次新的 commit，替代上一次提交
# 如果代码没有发生任何变化，则用于改写上一次 commit 的提交信息
git commit --amend -m <message>

# 重做上一次 commit，并包括指定文件的新变化
git commmit --amend <file1> <file2> ...
```

### 1.5. Git 分支

```shell
# 显示所有本地分支
git branch 

# 列出所有远程分支
git branch -r

# 列出所有本地分支和远程分支
git branch -a

# 新建分支，但依然留在当前分支
git branch <branch-name>

# 新建分支，并与指定的远程分支建立追踪关系
git branch --track <branch> <remote-branch>

# 删除分支
git branch -d <branch-name>

# 删除远程分支
git push origin --delete <branch-name>
git branch -dr <remote/branch>

# 新建分支，并切换到该分支
git checkout -b <branch>

# 切换到指定分支，并更新工作区
git checkout <branch-name>

# 切换到上一个分支
git checkout -

# 建立追踪关系，在现有分支与指定远程分支之间
git branch --set-upstream <branch> <remote-branch>

# 合并指定分支到当前分支
git merge <branch>

# 衍合指定分支到当前分支
git rebase <branch>

# 选择一个 commit，合并进当前分支
git cherry-pick <commit>
```

### 1.6. Git 标签

```shell
# 列出所有本地标签
git tag 

# 基于最新提交创建标签
git tag <tag-name>

# 删除标签
git tag -d <tag-name>

# 删除远程标签
git push origin :refs/tags/<tag-name>

# 查看 tag 信息
git show <tag>

# 提交指定 tag
git push [remote] <tag>

# 提交所有 tag
git push [remote] --tags

# 新建分支，并指向某个 tag
git checkout -b <branch> <tag>
```

### 1.7. Git 信息查看

```shell
# 显示有变更的文件
git status 

# 显示当前分支的版本历史
git log 

# 显示commit历史，以及每次commit发生变更的文件
git log --stat

# 根据关键词，搜索提交历史
git log -S <keyword>

# 显示某个commit之后的所有变动，每个commit占一行
git log <tag> HEAD --pretty=format:%s

# 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
git log <tag> HEAD --grep <feature>

# 显示某个文件的版本历史，包括文件改名
git log --follow <file>
git whatchanged <file>

# 显示指定文件相关的每一次 diff
git log -p <file>

# 显示过去5次提交
git log -5 --pretty --oneline 

# 显示所有提交过的用户，按提交次数排序
git shortlog -sn

# 显示指定文件是什么用户在什么时间修改过
git blame <file>

# 显示暂存区和工作区的差异
git diff

# 显示暂存区和上一次 commit 的差异
git diff --cached <file>

# 显示工作区与当前分支最新commit之间的差异
git diff HEAD

# 显示两次提交之间的差异
git diff <first-branch>...<second-branch>

# 显示今天写了多少代码
git diff --shortstat "@{0 day ago}"

# 显示某次提交的 meta-data 和内容变化
git show <commit>

# 显示某次提交发生变化的文件
git show --name-only <commit>

# 显示某次提交时，某个文件的内容
git show <commit>:<filename>

# 显示当前分支的最近几次提交
git reflog
```

### 1.8. Git 远程操作

```shell
# 下载远程仓库的所有变动
git fetch <remote>

# 取回远程仓库的变化，并与本地分支合并
git pull <remote> <branch>

# 显示所有远程仓库
git remote -v

# 显示某个远程仓库的信息
git remote show <remote>

# 增加新的远程仓库，并命名
git remote add <shortname> <url>

# 上传本地指定分支到远程仓库
git push <remote> <branch>

# 强行推送当前分支到远程仓库，即使有冲突
git push <remote> --force

# 推送所有分支到远程仓库
git push <remote> --all

# 删除远程分支或标签
git push <remote>:<branch/tag-name>

# 上传所有标签
git push --tags
```

### 1.9.Git 操作撤销

```shell
# 撤销工作目录中所有未提交文件的修改内容
git reset --hard HEAD

# 撤销指定的未提交文件的修改内容
git checkout HEAD <file>

# 撤销指定的提交
git revert <commit>

# 退回到之前1天的版本
git log --before="1 days"

# 恢复暂存区的指定文件到工作区
git checkout <file>

# 恢复某个 commit 的指定文件到暂存区和工作区
git checkout <commit> <file>

# 恢复暂存区的所有文件到工作区
git checkout .

# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
git reset <file>

# 重置暂存区与工作区，与上一次commit保持一致
git reset --hard

# 重置当前分支为指定commit，同时重置暂存区，但工作区不变
git reset <commit>

# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
git reset --hard <commit>

# 重置当前分支的HEAD为指定commit，但暂存区和工作区保持不变
git reset --keep <commit>

# 新建一个commit，用于撤销指定comm
# 后者的所有变化都将被前者抵消，并应用到当前分支
git revert <commit>

# 暂时将未提交的变化移除，稍后再移入
git stash
git stash pop
```

## 2. Git 其它

```shell
# 查看文件的修改历史
git log -p <file>
# 如：
git log -p README.md

# 搜索符合条件的历史
git log -S'PATTERN'
# 如：
git log -S'stupid'

# 交互式保存与取消保存的变化
git add -p

# 只删除远程文件，但不影响本地文件
# 对于删除已经推送过的忽略文件记录而且不影响本地文件是非常的方便
git rm --cached <file>

# 返回某个非HEAD分支的提交记录
git log ..BRANCH
# 如：
# 返回全部 master 分支的历史记录，包括未被合并到当前分支的提交几率
git log ..master

# 返回已合并分支列表或未合并的分支列表
git branch –merged
git branch –no-merged

# 返回包含某个指定 SHA 的分支列表
git branch –contains SHA
# 如：
# 显示全部包含提交 2f832b 的分支
git branch --contains 2f8e2b

# 返回简单版的 git status
git status -s

# 显示本地已完成的操作
git reflog

# 显示提交记录的参与者列表
git shortlog -sn
```