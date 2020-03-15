# git

## 一、介绍:

   **Git\(读音为/gɪt\)是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到非常大的项目版本管理。** **\[1\] Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。    当多人开发过程中,git 能够很好的管理代码,能够对代码历史追溯。**

## 二、专有名词:

   **○ workspace:    工作区    ○ Index/Stage:    暂存区    ○ Repository:    仓库区\(或者是本地仓库\)    ○Remote:    远程仓库**

## 三、专有名词详解:

### ①  工作区

      **程序员进行开发改动的地方,是你当前看到的, 也是最新的。**       **平常我们开发就是拷贝远程仓库中的一个分支，基于该分支进行开发。在开发的过程中就是对工作区操作。**

### ②  暂存区

      **.git目录下的index文件,暂存区会记录`git add` 添加的文件的相关文件的信息\(文件名、大小、timestam... \),不保存文件实体,通过id指向每个文件的实体。可以使用`git status`查看暂存区的状态。暂存区标记了你当前工作区中,那些内容是被git管理。**       **当你在完一个需求之后需要去需要提交到远程仓库，那么第一步就是通过`git add`先提交到暂存区,被git管理。**

### ③  本地仓库

      **保存了对象提交过的各个版本，比起工作区和暂存区的内容，它要更旧一些。                                     `git commit`后同步index的目录树到本地仓库,方便从下一步通过`git push`同步本地仓库和远程仓库的同步。**

### ④  远程仓库

**远程仓库的内容可能被分布在多个地点的处于协作关系的本地仓库修改，因此他可能与本地仓库同步，也可能不同步，但是他的内容是最旧的。**

## 四、 常用的git命令:

## 将远程的代码下载到本地:

_**分支介紹：**_

```text
 master   ：  默认开发分支
 Head     :   默认开发分支
 origin   :   默认远程版本库
 Head^    :   Head 的父提交
```

_**创建版本库:**_

```text
$ git clone  <repurl> #克隆远程版本库
$ git init            #初始化本地版本库
```

_**修改和提交:**_

```text
$ git status  #查看状态
$ git diff    #查看变更内容
$ git add     #跟踪所有改动的文件
$ git add <file> #跟踪指定的文件
$ git mv <old> <new> #文件改名
$ git rm <file> #删除文件
$ git rm --cached <file> #停止跟踪文件但不删除
$ git commit -m  "Commit Message" #提交所有更新过的文件
$ git commit --amend # 修改最后一次提交
```

_**查看提交历史:**_

```text
$ git log # 查看提交历史
$ git log -p <file>  #查看指定文件的提交历史
$ git blame <file> #以列表的方式查看指定文件的提交历史
```

_**撤销:**_

```text
$ git reset --hard HEAD # 撤销工作目录中所有未提交文件的修改内容
$ git checkout HEAD <file> #撤销指定的未提交文件的修改内容
$ git revert <commit> # 撤销指定的提交
```

_**分支与标签:**_

```text
$ git beanch #显示所有本地分支
$ git checkout <branch/tag> # 切换到指定分支或标签
$ git beanch <new-branch> # 创建新分支
$ git beanch -d <branch> # 删除本地分支
$ git tag # 列出所有本地标签
$ git tag <tagname> # 基于最新提交创建标签
$ git tag -d <tagname> # 删除标签
```

_**合并与衍合:**_

```text
$ git merge <beanch> # 合并指定分支到本分支
$ git rebase <beanch> # 衍合指定分支到本分支
```

_**远程操作:**_

```text
$ git remote -v # 查看远程版本库信息
$ git remote show <remote> # 查看指定远程版本库信息
$ git remote add <remote> <url> # 添加远程版本库

$ git fetch <remote> #从远程库获取代码
$ git pull <remote> <beanch> # 下载代码及快速合并
$ git push <remote> <beanch> # 上传代码及快速合并
$ git push <remote> : <branch/tag-name> # 删除远程分支或标签
$ git push -- tags # 上传所有标签
```

add:

| 命令 | 描述 |
| :--- | :--- |
| git add . | 添加当前目录的所有文件到暂存区 |
| git add \[dir\] | 添加指定目录到暂存区,包括子目录 |
| git add \[file 1 \] | 添加指定文件到暂存区 |

commit:

| 命令 | 描述 |
| :--- | :--- |
| git commit -m \[message\] | 提交暂存区到本地仓库,message代表说明信息 |
| git commit \[file1\] -m \[message\] | 提交暂存区的指定文件到本地仓库 |
| git commit  -- amend -m \[mesage\] | 使用一次新的commit ,替代上一次提交 |

beanch :

| 命令 | 描述 |
| :--- | :--- |
| git beanch | 列出所有本地分支 |
| git beanch -r | 列出所有的远程分支 |
| git beanch -a | 列出所有的本地分支和远程分支 |
| git beanch \[branch-name\] | 新建一个分支,但依然停留在当前分支 |
| git checkout --track \[branch\]\[remote-branch\] | 新建一个分支,与指定的远程分支建立追踪关系 |
| git checkout -b  \[branch-name\] | 新建一个分支,并切换到该分支 |
| git -checkout   \[branch-name\] | 切换到指定分支,并更新工作区 |
| git -beanch  - d \[branch-name\] | 删除分支 |
| git push origin --delete  \[branch-name\] | 删除远程分支 |

后续根据理解添加对git 的资料追加!

