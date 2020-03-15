# 开始添置物品到房间内部

## 基本操作

* git init -- 初始化仓库：
  * 要使用 Git 进行版本管理，必须先初始化仓库。Git 是使用 git init 命令尽心初始化的。

    ```text
          mkdir git-totorial
          cd git-totorial
          git init
    ```
* git status -- 查看仓库的状态：
  * git status 命令用于显示 git 仓库的状态。
* git add -- 向暂存区中添加文件：
  * 如果只是用 Git 仓库的工作树创建了文件，那么该文件并不会被标记入 Git 仓库的版本管理对象中。因此我们使用 git status 命令查看新的文件时，他会显示在 Untracked files 中。要想让文件成为 Git 仓库的管理对象，就要用 git add 命令将其加入到暂存区中。暂存区是提交之前的一个临时区域。通过 git add . 添加之后，再使用 git status 查看仓库的状态，发现文件出现在了 Changes to be committed 中。
* git commit -- 保存仓库的历史记录：
  * git commit 命令可以将当前暂存区中的文件实际保存到仓库的历史记录中。通过这些记录，我们就可以在工作树中复原文件。
  * 记录一行提交信息

    ```text
          git commit -m  "描述的内容"
    ```

  * 终止提交
  * 查看提交后的状态

    ```text
          nothing to commit ,working directoty clen
    ```
* git log -- 查看提交日志：
  * git log 命令可以查看以往仓库中提交的日志。包括可以查看什么人在什么时候进行提交和合并操作。
  * 只显示提交信息的第一行

    ```text
      git log --pretty=short
    ```

  * 只显示指定目录，文件的日志
    * 只要在 git log 命令后加上目录名，便会只显示目录下的日志，如果加上文件名，就只会显示该文件的相关的日志。

      ```text
      git log readme.md
      ```
  * 显示文件的改动

    ```text
      git log -p readme.md
    ```
* git diff -- 查看更改前后的差别：
  * git diff 命令可以查看工作树，暂存区，最新提交之间的差别。

## 分支操作

* 定义：
  * 在进行多个并行作业时，我们会用到分支。在这类并行开发的过程中，往往同时存在多个最新代码的状态。例如：从master分支创建 feature-A 和 fix-B 分支后，每个分支都拥有自己的最新代码，master 分支是 Git 默认创建的分支，因此基本上所有的开发都是以这个为中心开发。
* git branch -- 显示分支一览表
  * git branch 命令可以将分支名列表显示。同时可以确认所在分支。
* git checkout -b -- 创建，切换分支
  * 如果想以当前的 master 分支为基础创建新的分支，我们需要用到 git checkout -b 命令。
  * 切换到 feature-A 分支并进行提交

    ```text
          git check -b feature-A
    ```

  * 切换到 master 分支

    ```text
          git checkout master
    ```
* git merge -- 合并分支
  * 我们假设分支 feature-A 已经开发完成，想要将它合并到主分支中，首先切换到master分支。

    ```text
          git checkout master
    ```

  * 然后合并feature-A分支。为了在历史记录中明确记录下本次分支合并，我们需要创建合并提交。因此，在合并时加上 --no-ff 参数。

    ```text
          git merge --no-ff feature-A
    ```

  * 随后编辑器会启动，用于录入合并提交信息
    * 默认信息中包含了从 feature-A 分支合并的相关内容，所以可以不用修改，将内容保存，关闭编辑器，然后会看到下面的结果

      ```text
            Merge made by the 'recursivr' strategy
            README.md | 2++
            1 file changed,2 insertions(+)
      ```

      这样一来 feature-A 就合并到master中了。

## 更改提交的操作

* git reset -- 回溯历史版本
  * 将代码还原到以前的版本
  * 回溯到创建 feature-A 分支之前
    * 使用 git reset --head 命令，只要提供目标时间点的哈希值，就可以完全恢复到该时间点的状态。

      ```text
            git  reset --hard xxxxxx
      ```
  * 创建 fix-b 的特性分支：
    * 略
  * 将 master 恢复到 feature-A 分支合并之后的状态。
  * 消除冲突
    * 将 fix-b merge 到 master 分支时，系统会说文件有了冲突，点开冲突的文件。
      * ======= 以上的部分是当前的 head 内容，下面的部分要合并的 fix-b 的内容。
  * 提交解决后的结果
    * 解决冲突之后，执行 git add 命令和git commit 命令。
* git commit --amend -- 修改提交信息
  * 执行 git commit --amend 命令之后，会打开编辑器，将内容修改好之后，关闭编辑器。
* git rebase -i -- 压缩历史
  * 执行命令：

    ```text
          git rebase -i HEAD-2
    ```

  * 文件中会出现：

    ```text
          pick 7a34294 add feature-C
          pick 6fba227 Fix typo
          .....
    ```

    * 我们将 6fba227 合并到 add feature-C 中，将 6fba227 左侧 pick 删除，改为 fixup ,保存，关闭编辑器。

## 推送到远程的仓库

* git remote add -- 添加远程仓库

  ```text
        git  remote add origin  仓库的链接
  ```

* git push -- 推送到远程仓库

  ```text
        git push -u origin master
  ```

## 从远程的仓库获取

* git clone -- 获取远程仓库

  ```text
        git clone 仓库的网络地址
  ```

* git pull -- 获取远程最新的代码

  ```text
        git pull
  ```

