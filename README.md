# git学习记录

### 1. 克隆远程仓库
git clone
```bash
git clone git@github.com:rdzfv/gitLearning.git
```
### 2. 添加新的文件，修改，并进行第一次提交
```bash
git add README.md  #将文件的本次修改至提交暂存区
git commit -m "init commit"
git branch -M master  #重命名本地当前分支 git branch (-m | -M) [<oldbranch>] <newbranch>
git push -u origin master  #将本地commit提交到远端仓库的master分支，-u为指定上游
```
### 3. 编写.gitignore并提交
.gitignore的写法说明见.gitignore文件
```bash
git add .  #添加了.gitignore文件后，add操作不需要指定具体文件，.gitignore规定的文件之外都会被add
git commit -m "feat:添加了.gitignore"
git push
```
### 4. 撤销commit
```bash
git commit -a -m "feat:错误的提交"  #在commit中加-a可以跳过暂存
git commit --amend -m "feat:撤销错误的commit，并提交正确的commit"
```

### 5. 回退提交
如果你有一个"脏"提交，想要回退到这个提交前的状态；但保留脏提交的修改。
```bash
git reset --soft HEAD^  #--soft表示只重置头部; HEAD^表示HEAD前的一个提交状态
```
如果你有一个"脏"修改的提交，想要discard所有的修改，回到提交前的状态
```bash
git reset --hard HEAD^  #--hard表示硬撤销，会丢失untracked files
```

### 6. 合并两个分支
再创建一个工作分支
```bash
git checkout -b develop2 #checkout -b = branch + checkout
```
一部分的工作在develop2中完成，并提交
```bash
git commit -a -m "feat:develop2分支上的提交"
```