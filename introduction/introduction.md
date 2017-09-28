#introduction
## 如何从github上克隆项目到本地电脑
使用命令 git clone
git clone <remote address>

## 如何查看项目状态
使用命令 git status

## git的文件存储原理
文件存储分三个区域: 工作区、暂存区、版本库
工作区中所有的文件改动都需要先经过暂存区再放入版本库中

### 工作区到暂存区
使用命令 git add
git add <file>
git add .

### 暂存区到版本库
使用命令 git commit -m ''

## 如何查看各个区域之间的差异
### 查看工作区与暂存区之间的差异
使用命令 git diff

### 查看暂存区与版本库之间的差异
使用命令 git diff --cached
        git diff --staged

### 查看工作区与版本库之间的差异
使用命令 git diff <branchName>

## 提交到版本库
使用命令 git commit -m ''

## git的撤销
撤销分为三种情形
1. 从暂存区中撤销
使用命令 git reset HEAD <file>
这样操作之后就会将暂存区中指定的文件还原回工作区 也就是说该文件的改动记录不会被保存记录
2. 从工作区中撤销
使用命令 git checkout -- <file>
这样操作之后就会将工作区中指定的文件修改内容还原 也就是说文件内容会与版本库中的文件内容一致
3. 撤销上一次的提交
使用命令 git commit -m 'description' --amend
将上一次的commit操作撤销 然后与本次修改的内容一起进行提交

## 查看提交记录
使用命令 git log

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
3. 查看最新的git提交操作
使用命令 git reflog