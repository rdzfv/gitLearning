# git学习记录

### 1. 克隆远程仓库
git clone
```bash
git clone git@github.com:rdzfv/gitLearning.git
```
### 2. 添加新的文件，修改，并进行第一次提交
```bash
git add README.md  #添加文件至提交暂存区
```
```bash
git commit -m "init commit"
```
```bash
git branch -M master  #重命名本地当前分支 git branch (-m | -M) [<oldbranch>] <newbranch>
```
```bash
git push -u origin master  #将本地commit提交到远端仓库的master分支，-u为指定上游
```