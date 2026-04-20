# Git CheatSheet | Git 命令速览与备忘清单

对于新手而言，在日常工作中还是尽量使用 [SourceTree]()、[GitHub Desktop]()等 界面工具，避免意外操作。

# 常用脚本

- 快速提交

```sh
# !/bin/bash

git add --all
git commit -m "feat: ${1:=update articles or snippets}" --no-verify
git pull
git push
```

# Configuration | 配置

## Management | 配置管理

```sh
# 列举所有的别名与配置
git config --list

# Git 别名配置
git config --global alias.<handle> <command> git config --global alias.st status

# 设置 Git 为大小写敏感
git config --global core.ignorecase false
```

我们也可以查看常用的辅助查询命令：

```sh
# 在 Git 命令行里查看 everyday git
git help everyday

# 显示 git 常用的帮助命令
git help -g

# 获取 Git Bash 的自动补全
curl http://git.io/vfhol > ~/.git-completion.bash && echo '[ -f ~/.git-completion.bash ] && . ~/.git-completion.bash' >> ~/.bashrc

# 设置自动更正
git config --global help.autocorrect 1
```

## User | 用户配置

```sh
# 配置 HTTP 代理
git config --global http.proxy http://127.0.0.1:1080
git config --global https.proxy https://127.0.0.1:1080

# 配置 Socks 代理
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'

# 取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy
git config --global http.sslVerify false
```

```sh
gitalias['alias.cp']='cherry-pick'
gitalias['alias.st']='status -sb'
gitalias['alias.cl']='clone'
gitalias['alias.ci']='commit'
gitalias['alias.co']='checkout'
gitalias['alias.br']='branch'
gitalias['alias.dc']='diff --cached'
gitalias['alias.lg']="log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %Cblue<%an>%Creset' --abbrev-commit --date=relative --all"
gitalias['alias.last']='log -1 --stat'
gitalias['alias.unstage']='reset HEAD --'
```

# Repository | 仓库配置与管理

## Manipulation | 操作

初始化某个仓库：

```sh
# 初始化一个版本仓库
git init

#Clone远程版本库
git clone git@xbc.me:wordpress.git
git clone https://username@github.com/username/repository.git

# 添加远程版本库origin，语法为 git remote add [shortname] [url]
git remote add origin git@xbc.me:wordpress.git

# 查看远程仓库
git remote -v
```

查看远端仓库相关信息：

```sh
# 获取所有远端引用配置
git remote
# 或者
git remote show

# 修改某个远端的地址
git remote set-url origin <URL>
```

查看仓库的统计信息：

```sh
# 查看当前仓库中的所有未打包的 objects 和磁盘占用
git count-objects --human-readable

# 从 object 数据库中删除所有不可达的 object
git gc --prune=now --aggressive
```

## .gitignore

注意忽略只对未跟踪文件有效，对于已加入版本库的文件无效，Git 内置三级忽略文件机制：

- 版本库共享式忽略文件，版本库中目录下的 .gitignore 文件作用于整个目录及子目录，会随着该版本库同其他人共享。

- 本地的针对具体版本库的独享式忽略文件，即在版本库 .git 目录下的文件 info/exclude 中设置文件忽略

- 本地的全局的独享式忽略文件，通过 Git 的配置变量 core.excludesfile 指定的一个忽略文件(指定文件名)，其设置的忽略对所有本地版本库均有效。设置方法如下(文件名可以任意设置)：

```sh
git config --global core.excludesfile ~/.gitignore
```

Git 的忽略文件遵循以下语法规则：

- 忽略文件中的空行或以井号(#)开始的行将会被忽略。
- 可以使用 Linux 通配符。例如：星号(\*)代表任意多个字符，问号(？)代表一个字符，方括号([abc])代表可选字符范围，大括号({string1,string2,...})代表可选的字符串等。
- 如果名称的最前面有一个感叹号(!)，表示例外规则，将不被忽略。
- 如果名称的最前面是一个路径分隔符(/)，表示要忽略的文件在此目录下，而子目录中的文件不忽略。
- 如果名称的最后面是一个路径分隔符(/)，表示要忽略的是此目录下该名称的子目录，而非文件(默认文件或目录都忽略)。

# Commit | 提交

```sh
# 管道命令，可用于脚本
$ git diff-tree --no-commit-id --name-only -r bd61ad98

# 查看某次提交中修改的文件
$ git show --pretty="" --name-only bd61ad98
```

## Tracking | 追踪

查看当前追踪的文件信息

```sh
# 展示所有被追踪的文件
git ls-files -t

# 展示所有未被追踪的分支
git ls-files --others

# 展示所有被忽略的文件
git ls-files --others -i --exclude-standard
git check-ignore *
git status --ignored
```

```sh
# 从工作目录中删除文件，同时会暂存信息
$ git rm [file]

# 从版本控制中移除该文件
$ git rm --cached [file]

# 本地重命名并且提交
$ git mv [file-original] [file-renamed]
```

## Stash | 贮存

git stash -- The command saves your local modifications away and reverts the working directory to match the HEAD commit. It allows you to store your uncommited modifications into a buffer area called stash, and deletes it from the branch you are working on. You may later retreive them by applying the stash.

## Undo | 撤销

# Branch | 分支

Git 中的分支实际上只是 Commit 指针。

```sh
# 命令行中查看版本树
$ git log --pretty=oneline --graph --decorate --all

# 内置的可视化界面查看版本树
$ gitk --all

# 根据提交人过滤 Commit 信息
$ git log --author="username" --pretty=format:"%h - %an, %ar : %s"
```

## Manipulation | 操作

```sh
# 创建某个分支
git branch BRANCH_NAME

# 创建并且切换到某个分支
git checkout -b BRANCH_NAME
```

### Head

分支是

## Merge | 分支合并

--force 会使用本地分支的提交覆盖远端推送分支的提交。也就是说，如果其他人在相同的分支推送了新的提交，你的这一举动将“删除”他的那些提交！就算在强制推送之前先 fetch 并且 merge 或 rebase 了也是不安全的，因为这些操作到推送之间依然存在时间差，别人的提交可能发生在这个时间差之内。使用此参数推送，如果远端有其他人推送了新的提交，那么推送将被拒绝，这种拒绝和没有加 --force 参数时的拒绝是一样的。

### cherry-pick

git cherry-pick 可以选择某一个分支中的一个或几个 commit(s) 来进行操作，譬如我们存在多个稳定开发版本，在不能完全合并分支的情况下又想把某些功能合入到某个分支，那就可以利用 cherry-pick 对已经存在的 commit 进行再次提交。注意，当执行完 cherry-pick 以后，将会生成一个新的提交；这个新的提交的哈希值和原来的不同，但标识名一样。

```sh
# 选择某个其他分支的 commit 合并到当前分支
$ git cherry-pick <commit id>

# 如果出现冲突，则类似于 Rebase 进行解决
# 手动查看冲突文件
$ git status

# 设置文件已经解决冲突
$ git add ...

# 设置 cherry-pick 继续执行
$ git cherry-pick --continue
$ git cherry-pick --quit
$ git cherry-pick --abort
```

## Rebase

顾名思义，Rebase(变基)有移花接木之效果，能将特性分支移接到主分支之上，常用于优化提交历史，或者修改本地的提交信息。

首先查看本地的 Commit 历史：

```sh
$ git log --pretty=oneline

a931ac7c808e2471b22b5bd20f0cad046b1c5d0d c
b76d157d507e819d7511132bdb5a80dd421d854f b
df239176e1a2ffac927d8b496ea00d5488481db5 a
```

运行 Git Rebase:

```sh
# 使用 Git Rebase，对最后两个提交进行操作
git rebase --interactive HEAD~2
```

```s
pick b76d157 b
squash a931ac7 c //change pick to squash

# Rebase df23917..a931ac7 onto df23917
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#
# If you remove a line here THAT COMMIT WILL BE LOST.
# However, if you remove everything, the rebase will be aborted.
#
```

and save-quitting your editor, you’ll get another editor whose contents are

```s
# This is a combination of 2 commits.
# The first commit's message is:

b

# This is the 2nd commit message:

c
```

done

```sh
$ git log --pretty=oneline
18fd73d3ce748f2a58d1b566c03dd9dafe0b6b4f b and c
df239176e1a2ffac927d8b496ea00d5488481db5 a
```

# Workflow | 协作

## Commit Message | 提交信息规范

目前规范使用较多的是 [Angular 团队的规范](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md%23-git-commit-guidelines), 继而衍生了 [Conventional Commits specification](https://conventionalcommits.org/). 很多工具也是基于此规范, 它的 message 格式如下:

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

我们通过 git commit 命令带出的 vim 界面填写的最终结果应该类似如上这个结构, 大致分为三个部分(使用空行分割):

- 标题行: 必填, 描述主要修改类型和内容
- 主题内容: 描述为什么修改, 做了什么样的修改, 以及开发的思路等等
- 页脚注释: 放 Breaking Changes 或 Closed Issues

分别由如下部分构成:

- type: commit 的类型
  - feat: 新特性
  - fix: 修改问题
  - refactor: 代码重构
  - docs: 文档修改
  - style: 代码格式修改, 注意不是 css 修改
  - test: 测试用例修改
  - chore: 其他修改, 比如构建流程, 依赖管理.
- scope: commit 影响的范围, 比如: route, component, utils, build...
- subject: commit 的概述, 建议符合 [50/72 formatting](https：//stackoverflow.com/questions/2290016/git-commit-messages-50-72-formatting)
- body: commit 具体修改内容, 可以分为多行, 建议符合 [50/72 formatting](https：//stackoverflow.com/questions/2290016/git-commit-messages-50-72-formatting)
- footer: 一些备注, 通常是 BREAKING CHANGE 或修复的 bug 的链接.

这样一个符合规范的 commit message, 就好像是一份邮件。如果你只是个人的项目, 或者想尝试一下这样的规范格式, 那么你可以为 git 设置 commit template, 每次 git commit 的时候在 vim 中带出, 时刻提醒自己:

修改 ~/.gitconfig, 添加:

```
[commit]
template = ~/.gitmessage
```

新建 ~/.gitmessage 内容可以如下:

```
# head: <type>(<scope>): <subject>
# - type: feat, fix, docs, style, refactor, test, chore
# - scope: can be empty (eg. if the change is a global or difficult to assign to a single component)
# - subject: start with verb (such as 'change'), 50-character line
#
# body: 72-character wrapped. This should answer:
# * Why was this change necessary?
# * How does it address the problem?
# * Are there any side effects?
#
# footer:
# - Include a link to the ticket, if any.
# - BREAKING CHANGE
#
```

## Merge Request

推荐团队中采用 Merge Request 的方式进行协作开发，即基于主分支 clone 之后再合并回去：

```js
git checkout dev
git pull --rebase --prune
git checkout -b feat/x # or fix/y

# coding time

# may commit several times
git commit -m ''

# make sure rebase from origin dev branch
git fetch
git rebase origin/dev
git push # maybe `-f` flag is required if you've pushed before rebase

# create Merge Request to dev branch

# code changes according MR review

# confirm to rebase again in case others merged before your MR
git fetch
git rebase origin/dev
git push
```

## Statistics | 统计数据

```sh
# 查看 Git 上的个人代码量，username 需要修改为真实用户名
$ git log --author="username" --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }' -
# added lines: 120745, removed lines: 71738, total lines: 49007

# 统计每个人增删行数
git log --format='%aN' | sort -u | while read name; do echo -en "$name\t"; git log --author="$name" --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }' -; done

# 统计提交数前五名
$ git log --pretty='%aN' | sort | uniq -c | sort -k1 -n -r | head -n 5
```

# Links

- https://learnxinyminutes.com/docs/zh-cn/git-cn/
- https://gist.github.com/eashish93/3eca6a90fef1ea6e586b7ec211ff72a5
