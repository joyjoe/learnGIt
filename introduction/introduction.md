#introduction
## 如何从github上克隆项目到本地电脑
使用命令 git clone
git clone <remote address>

## 配置git
git配置中最重要的两条
git config --global user.name
git config --global user.email

## .gitignore文件
.gitignore文件的作用是可以配置哪些文件不会被加入到版本控制中
*~ 表示以~结尾的临时文件
log/\*.log 表示log文件夹下以log为扩展名的所有文件

## 如何查看项目状态
使用命令 git status
如果只需要简略查看项目状态可以添加参数 -s
使用命令 git status -s 或者 git status --short
运行结果中各字符的含义
?? 表示该文件是新增的，还没有被跟踪
A  表示新添加到暂存区的文件
_M 表示该文件在工作区中被修改过，但是还没有被加入到暂存区中
M_ 表示该文件在工作区中被修改过，并且被加入到暂存区中
MM 表示该文件在修改并提交到暂存区之后，又在工作区中被修改过


## git的文件存储原理
文件存储分三个区域: 工作区、暂存区、版本库
工作区中所有的文件改动都需要先经过暂存区再放入版本库中

### 工作区到暂存区
使用命令 git add
git add <file>
git add .

### 提交到版本库
提交到版本库分两种情形
1. 将工作区中的文件修改内容保存在暂存区中之后再提交到版本库中
使用命令 git commit -m ''
2. 直接将工作区中的文件修改内容跳过暂存区而直接提交到版本库中
使用命令 git commit -a -m ''

## 如何查看各个区域之间的差异
### 查看工作区与暂存区之间的差异
使用命令 git diff

### 查看暂存区与版本库之间的差异
使用命令 git diff --cached
        git diff --staged

### 查看工作区与版本库之间的差异
使用命令 git diff <branchName>

### 如何使用插件更好地展示差异
使用命令 git difftool --tool -help
先查看当前系统中所支持的Git Diff插件
使用命令 git difftool --tool=<plugin>


## git的撤销
撤销分为三种情形
1. 从暂存区中撤销
使用命令 git reset HEAD <file>
这样操作之后就会将暂存区中指定的文件还原回工作区 也就是说该文件的改动记录不会被保存记录
2. 从工作区中撤销
使用命令 git checkout -- <file>
这样操作之后就会将工作区中指定的文件修改内容还原到与暂存区中的文件内容一致
3. 撤销上一次的提交
使用命令 git commit -m 'description' --amend
将上一次的commit操作撤销 然后与本次修改的内容一起进行提交

## 查看提交记录
使用命令 git log
添加参数 -p 可以查看每次提交时的差异
添加参数 -N 可以查看最近N次的提交记录
添加参数 --stat 可以查看每次提交时的文件变化统计
添加参数 --pretty 可以指定信息显示的不同方式 如 oneline short full fuller
### 如果需要查看某一次提交的详细信息
使用命令 git show commitID

## 删除文件
删除文件也分三种情形
1. 从暂存区中删除已经在工作区中不存在的文件
使用命令 git rm <file>
2. 从暂存区和工作区中均删除工作区中存在的文件
使用命令 git rm -f <file>
3. 从暂存区中删除已提交暂存的工作区文件
使用命令 git rm --cached <file>

## git的还原
1. 将工作区中的某个文件的内容还原为某个提交版本
使用命令 git checkout commitid <file>
2. 将工作区中的所有文件的内容还原为某个提交版本
使用命令 git reset --hard commitid
HEAD 表示当前指针头部的commitid
HEAD^ 表示当前指针头部沿着提交链条往前移动一次
HEAD~ 表示当前指针头部沿着提交链条往前移动一次
HEAD~n 表示当前指针头部沿着提交链条往前移动n次
3. 查看最新的git提交操作
使用命令 git reflog

## 文件更名
如果有文件需要更名 使用命令 git mv oldfile newfile


## 代码上传
如何将代码上传到github的远程仓库中
使用命令 git push
先通过 git remote -v查看远程仓库信息
git remote 查看远程仓库的名字
再通过git push <repository> <branch>
将本地branch分支上的内容上传到远程仓库中

## 从远程仓库如何拉取新的更新代码
### 使用命令 git fetch
使用该命令之后接着使用 git diff <local-branch> <repository/branch>查看本地代码与远程仓库代码的区别
通过手动修改代码解决两者之间的冲突
最后使用命令 git merge <repository/branch> 来合并不同仓库中的代码以达到可以使用git push操作的条件

### 使用命令 git pull
