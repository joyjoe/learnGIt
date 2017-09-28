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