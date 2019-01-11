---
title: Git Related
---

# Git 安装

### Linux

- Linux用户可以在命令行输入`git`测试Git的安装
- 一般Linux自带git的，如果没有安装，则运行下列命令

```bash
sudo apt-get update
sudo apt-get install git-all
```

### Windows

- 前往`https://git-scm.com/download/win`下载`64-bit Git for Windows Setup`
- 下载后运行安装程序
- 点击一次`Next`后，勾选`Additional Icons`并点击`Next`
- 选择`Noptepad++`并点击`Next`
- 选择`Git from the command line and also from 3rd-party software`并点击`Next`
- 选择`Use the native Windows Secure Channel library`并点击`Next`
- 选择`Checkout Windows-style, commit Unix-style line endings`并点击`Next`
- 选择`Use MinTTY`并点击`Next`
- 勾选`Enable file system caching`和`Enable Git Credential Manager`并点击`Next`
- 点击`Install`开始安装
- 完成安装后运行`Git Bash`
- 执行下列命令

```bash
git config --global user.email "<Your Email Address>"
git config --global user.name "<Your Name>"
```

- 替换上面尖括号里面的内容为你自己的信息
- 之后的Git命令就可以在Git Bash里面执行了

<br>

Git Related Commands
======

<br>

Git Global Setup
------

``` bash
git config --global user.name "Lingxiao Duan"
git config --global user.email "duanlingxiao1219@sina.com"
```

<br>

Checking Status
------

``` bash
git status
```

<br>

.gitignore
------

+ All files in a directory
``` bash
/data/*
```

+ All files of one specific type
```
*.jpg
```

<br>

Version Control (Synchronizing)
------

+ Creating a new repository
``` bash
git clone git@9e5415541ac4:bigdata/processing.git
cd processing
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```

+ Setting up git to an existing folder
``` bash
cd existing_folder
git init
git remote add origin git@<git_address>:<group_name>/<project_name>.git
git add .
git commit -m "Initial commit"
git status
git push -u origin master
```

+ Setting up git to an existing repository
``` bash
cd existing_repo
git remote rename origin old-origin
git remote add origin git@<git_address>:<group_name>/<project_name>.git
git push -u origin --all
git push -u origin --tags
```

<br>

# Git常用指南

## 基本概念

- 工作区（当前的工作目录）
- 暂存区（Add等操作将修改保存至暂存区）
- 本地版本库（Commit操作将缓存区的修改提交到本地版本库）
- 远程版本库（本地版本push到远程版本库）

## 常用操作

### Git 常用命令使用

命令行里git的命令列表以及解释：

` git clone <address>`:复制代码库到本地

` git add `<file>` ...：添加文件到代码库中`
` git rm `<file>` ...：删除代码库的文件`
` git commit -m `<message>`：提交更改，在修改了文件以后，使用这个命令提交修改` 
` git pull：从远程同步代码库到本地。` 
` git push：推送代码到远程代码库。` 
` git branch：查看当前分支。带*是当前分支。` 
` git branch `<branch-name>`：新建一个分支。` 
` git branch -d `<branch-name>`：删除一个分支。` 
` git checkout `<branch-name>`：切换到指定分支。` 
` git log：查看提交记录（即历史的 commit 记录）。` 
` git status：当前修改的状态，是否修改了还没提交，或者那些文件未使用。` 
` git reset `<log>`：恢复到历史版本。`

代码库应该很好理解，就是存放代码的地方，而在 git clone 里，代码库一般指的是远程的代码库，即 github
给出的链接。而分支则是开发的一个阶段或者一个旁系版本，至于怎么定则取决于使用者了。例如，有一个分支叫做stable，代表里面的代码是经过测试的、稳定的；另一个分支叫dev，则是保存开发中的代码，不一定经过足够测试。

### 一般流程

1. 编辑文件，更新代码。
2. 添加代码到当前待提交的更改列表中：git add <修改的文件>
3. 提交当前修改作为一个记录：git commit -m '修改了<修改的文件>，原因是：……'
4. 更新代码：git push
5. 不要用git pull，用git fetch和git
   merge代替它，参考：http://longair.net/blog/2009/04/16/git-fetch-and-merge/。

### Git 分支操作

| 功能           | git命令                | IDEA操作                                                     |
| -------------- | ---------------------- | ------------------------------------------------------------ |
| 创建分支       | git branch feeder      | 项目右键 -\> git -\> Repository -\> Branches -\> New         |
| 查看当前分支   | git branch             | 项目右键 -\> git -\> Repository -\> Branches                 |
| git切换分支    | git checkout feeder    | 项目右键 -\> git -\> Repository -\> Branches -\> 选择分支    |
| 创建并切换语句 | git checkout -b feeder | 项目右键 -\> git -\> Repository -\> Branches -\> New Branch  |
| 合并分支       | git merge feeder       | 项目右键 -\> git -\> Repository -\> Merge changes -\> 选择要合并的分支 |
| 删除分支       | git branch -d feeder   | 项目右键 -\> git -\> Repository -\> Branches -\> 选择分支 =\> delete |

- [分支的新建与合并](https://git-scm.com/book/zh/v1/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%9A%84%E6%96%B0%E5%BB%BA%E4%B8%8E%E5%90%88%E5%B9%B6)

![分支](https://git-scm.com/figures/18333fig0316-tn.png)

### git 提交代码

| 功能                           | git命令                                                      | IDEA操作                                 |
| ------------------------------ | ------------------------------------------------------------ | ---------------------------------------- |
| **将工作区的修改提交到暂存区** | git add 提交 file 与其子目录/git add . 提交当前目录及所有子文件 | 项目右键 -\> git -\> add                 |
| **将暂存区内容提交到版本库**   | git commit 提交 file 与其子目录/git commit . 提交当前目录及所有子文件 | 项目右键 -\> git -\> Commit Directory    |
| **将本地分支推送到远程主机**   | git push <远程主机名> <本地分支名>:<远程分支名>              | 项目右键 -\> git -\> Repository -\> push |

### git 回退操作

| 功能                               | git命令                | IDEA操作                                        |
| ---------------------------------- | ---------------------- | ----------------------------------------------- |
| 改变暂存区的修改                   | git reset /git reset . | 项目右键 -\> git -\> Revert                     |
| 回退所有内容到上一个版本           | git reset HEAD^        | 项目右键 -\> git -\> Repository -\> resert Head |
| 回退a.py这个文件的版本到上一个版本 | git reset HEAD^ a.py   | 文件右键 -\> git -\> Repository -\> resert Head |

### git 拉取数据

| 功能                   | git命令                                         | IDEA操作                                  |
| ---------------------- | ----------------------------------------------- | ----------------------------------------- |
| 从远程拉取数据         | git pull <远程主机名> <远程分支名>:<本地分支名> | 项目右键 -\> git -\> Repository -\> pull  |
| 复制命令               | git clone ssh地址                               | 项目右键 -\> git -\> Repository -\> clone |
| 将远程主机更新取回本地 | git fetch <远程主机>                            | 项目右键 -\> git -\> Repository -\> fetch |

### 恢复命令 reset

#### reset命令有3种方式：

`git reset --mixed //此为默认方式，不带任何参数的git reset，即时这种方式，它回退到某个版本，只保留源码，回退commit和index信息` 
`git reset --soft  //回退到某个版本，只回退了commit的信息，不会恢复到index file一级。如果还要提交，直接commit即可` 
`git reset --hard  //彻底回退到某个版本，本地的源码也会变为上一个版本的内容`

#### 代码示例：

`git reset HEAD^         //回退所有内容到上一个版本`  
`git reset HEAD^ a.py    //回退a.py这个文件的版本到上一个版本 `  
`git reset --soft HEAD~3 //向前回退到第3个版本`  
`git reset --hard origin/master //将本地的状态回退到和远程的一样`  
`git reset 057d          //回退到某个版本 `  
`git revert HEAD         //回退到上一次提交的状态，按照某一次的commit完全反向的进行一次commit`

### 合并分支 merge

比如，如果要将开发中的分支（develop），合并到稳定分支（master），

`    首先切换的master分支：git checkout master。`  
`    然后执行合并操作：git merge develop。`  
`    如果有冲突，会提示你，调用git status查看冲突文件。`  
`    解决冲突，然后调用git add或git rm将解决后的文件暂存。`  
`    所有冲突解决后，git commit 提交更改。`

## 更改提交用户名/邮箱

`git config user.name "XXX"`  
`git config user.email "XXX"`  
`git config --global user.name "XXX"`  
`git config --global user.email "XXX"`

参考：

- <https://alvinalexander.com/git/git-show-change-username-email-address>

## 删除文件夹

`git checkout master`  
`git rm -r folder-name // 本地文件也删除`  
`git rm --cached file1.txt // 本地文件不删除，只删除git记录`  
`git commit -m "Remove duplicated directory"`  
`git push origin branch_name`

## 外部资料

- [Git 简单使用](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
- [Git Pro2](https://progit.bootcss.com/)
- [Github使用指南](https://github.com/NeuOL/neuola-legacy/wiki/github%E4%BD%BF%E7%94%A8%E6%8C%87%E5%8D%97)
- [git - 简明指南](http://rogerdudler.github.io/git-guide/index.zh.html)
- [Git版本控制与工作流](http://blog.jobbole.com/87410/)
- [ProGit](https://git-scm.com/book/zh/v2)
- [git-flow备忘清单](http://danielkummer.github.io/git-flow-cheatsheet/index.zh_CN.html)