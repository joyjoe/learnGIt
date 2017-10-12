# 入门级操作
## 配置git
git配置中最重要的两条
```
git config --global user.name
git config --global user.email
```
## 创建版本库
* 本地创建<br>
```
git init
```
* 克隆创建<br>
如何从github上克隆项目到本地电脑<br>
```
git clone
git clone <remote address>
```
* .gitignore文件<br>
.gitignore文件的作用是可以配置哪些文件不会被加入到版本控制中<br>
*~ 表示以~结尾的临时文件<br>
log/\*.log 表示log文件夹下以log为扩展名的所有文件

## 如何查看项目状态
使用命令 `git status`<br>
如果只需要简略查看项目状态可以添加参数 `-s`<br>
使用命令 `git status -s` 或者 `git status --short`<br>
运行结果中各字符的含义<br>
`??`表示该文件是新增的，还没有被跟踪<br>
`A `表示新添加到暂存区的文件<br>
`_M`表示该文件在工作区中被修改过，但是还没有被加入到暂存区中<br>
`M_`表示该文件在工作区中被修改过，并且被加入到暂存区中<br>
`MM`表示该文件在修改并提交到暂存区之后，又在工作区中被修改过<br>

## git的文件存储原理
文件存储分三个区域: **`工作区`**、**`暂存区`**、**`版本库`**
工作区中所有的文件改动都需要先经过暂存区再放入版本库中
### 将工作区的变化存储到暂存区
    git add <file>
    git add .
### 提交到版本库
提交到版本库分两种情形<br>
1. 将工作区中的文件修改内容保存在暂存区中之后再提交到版本库中<br>
```
git commit -m 'description'
```
2. 直接将工作区中的文件修改内容`跳过暂存区`而`直接提交到版本库`中<br>
```
git commit -a -m 'description'<br>
```
## 如何查看各个区域之间的差异
### 查看工作区与暂存区之间的差异
    git diff
    git diff HEAD -- filename
### 查看暂存区与版本库之间的差异
    git diff --cached
    git diff --staged

### 查看工作区与版本库之间的差异
    git diff <branchName>

### 使用插件更好地展示差异
```
git difftool --tool -help
```
如何查看当前系统中所支持的Git Diff插件<br>
```
git difftool --tool=<plugin>
```

## git的撤销
撤销分为三种情形
1. 从暂存区中撤销<br>
使用命令 `git reset HEAD <file>`<br>
这样操作之后就会将暂存区中指定的文件还原回工作区<br>也就是说该文件的改动记录不会被保存记录<br>
2. 从工作区中撤销<br>
使用命令 `git checkout -- <file>`<br>
这样操作之后就会将工作区中指定的文件修改内容还原到与暂存区中的文件内容一致
3. 撤销上一次的提交<br>
使用命令 ```git commit -m 'description' --amend```<br>
将上一次的commit操作撤销 然后与本次修改的内容一起进行提交

## 查看提交记录
使用命令 `git log`<br>
添加参数 `-p` 可以查看每次提交时的差异<br>
添加参数 `-N` 可以查看最近N次的提交记录<br>
添加参数 `--stat` 可以查看每次提交时的文件变化统计<br>
添加参数 `--pretty` 可以指定信息显示的不同方式 如 `oneline` `short` `full` `fuller`<br>
添加参数 `--graph` 可以查看分支合并图<br>
### 查看某一次提交的详细信息
    git show commitID

## 删除文件
* 分三种情形
1. 从暂存区中删除已经在工作区中不存在的文件<br>
`git rm <file>`
2. 从暂存区和工作区中均删除工作区中存在的文件<br>
`git rm -f <file>`
3. 从暂存区中删除已提交暂存的工作区文件<br>
`git rm --cached <file>`

## 还原
1. 将工作区中的某个文件的内容还原为某个提交版本<br>
`git checkout commitid <file>`

2. 将工作区中的所有文件的内容还原为某个提交版本<br>
**`git reset --hard commitid`**<br>
`HEAD` 表示当前指针头部的commitid
`HEAD^` 表示当前指针头部沿着提交链条往前移动一次
`HEAD~` 表示当前指针头部沿着提交链条往前移动一次
`HEAD~n` 表示当前指针头部沿着提交链条往前移动n次

3. 还原那些误删除的有效文件<br>
如果误操作删除了本来不该删除的文件<br>
使用 `git status -s` 会发现文件前面有个 D 符号<br>
此时可以通过使用 `git checkout <file>` 将误删除的文件重新找回来

4. 查看最新的git提交操作<br>
使用命令 `git reflog`


## 文件更名
如果有文件需要更名可以使用命令 `git mv oldfile newfile`

## 如何将本地仓库关联到远程仓库上
    git remote add <remoteRepository> <remoteRepositoryUrl>

## 代码上传
如何将代码上传到github的远程仓库中<br>
使用命令 `git push` 如果是第一次上传则添加 `-u` 参数<br>
先通过 `git remote -v`查看远程仓库信息
`git remote` 查看远程仓库的名字
再通过`git push <repository> <branch>`
将本地branch分支上的内容上传到远程仓库中
`git push -u origin master`
表示将本地仓库的master分支同步到远程一个名叫origin的仓库master分支上

## 从远程仓库如何拉取新的更新代码
### 使用命令 git fetch
使用该命令之后接着使用 `git diff <local-branch> <repository/branch>`查看本地代码与远程仓库代码的区别<br>
通过手动修改代码解决两者之间的冲突<br>
最后使用命令 `git merge <repository/branch>` 来合并不同仓库中的代码以达到可以使用git push操作的条件<br>

### 使用命令 git pull


## git分支管理
git创建分支命令 `git branch <branchName>`<br>
git切换分支命令 `git checkout <branchName>`<br>
两个命令可以合并成一个命令 `git checkout -b <branchName>`<br>
查看当前仓库里的分支,使用命令 `git checkout` 当前分支前面会有一个星号`※`<br>
删除分支命令 `git branch -d <branchName>`<br>
强行删除分支命令 ```git branch -D <branchName>```<br>

合并某分支到当前分支上使用命令 `git merge <branchName>`<br>

创建本地分支的同时也关联到远程仓库的某个分支 使用命令<br>
`git checkout -b <branchName> <remoteRepositoryName/branchName>`<br>
如何将本地分支与远程仓库中某个分支相互关联<br>
`git branch --set-upstream <branchName> <remoteRepositoryName/branchName>`<br>


## 解决分支合并时的冲突问题
使用git merge合并分支时，如果出现冲突，系统会提示CONFLICT。此时可以通过git status查看发生冲突的文件。然后修改文件内容以解决冲突。

## 分支合并的技巧
合并分支时，git会优先选择`fast-forward`模式。这样当删除掉合并分支后，该分支的所有消息都会消失。<br>
这时候可以使用`--no-ff`参数<br>
`git merge --no-ff -m 'commit info' <branchName>`表示master分支会多出一个提交id<br>

## 保存快照
如果你遇到下列情况就可以考虑使用该功能：当你正在自己的分支上搬砖时，突然有领导要求你赶紧放下手头工作去修复一个bug。可是你当前搬的砖还不够提交的，怎么办？此时就可以使用`git stash`命令保存你的快照。然后切换到别的分支上去搬砖。<br>
当你重新回到自己的分支上时，可以使用`git stash list`查看当前的所有快照。<br>
接着可以使用`git stash apply`将快照进行恢复，或者使用`git stash pop`取出快照。<br>
区别在于，前者需要使用`git stash drop`来删除快照。<br>

<hr>
更多git教程内容请参考[廖雪峰Git教程][1]

[1]: https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000 "浅显易懂的Git教程"
