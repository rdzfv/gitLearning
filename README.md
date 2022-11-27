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

### 6.创建开发分支并切换
```bash
git branch develop #在当前所在的提交对象上创建一个指针develop，此时HEAD还在当前分支
git checkout develop #将HEAD移到develop分支
git commit -a -m 'feat:develop分支提交测试'
```

### 7. 合并两个分支
再创建一个工作分支
```bash
git checkout -b develop2 #checkout -b = branch + checkout
```
一部分的工作在develop2中完成，并提交
```bash
git commit -a -m "feat:develop2分支上的提交"
```
一部分的工作在develop中完成，并提交
```bash
git checkout develop
git commit -a -m "feat:develop分支上的提交"
```
合并两个分支
```bash
git merge develop2
git commit -a -m "feat:合并develop分支和develop2分支，并解决冲突"
```
删除develop2分支
```bash
git branch -d develop2 #如果develop2还存在未合并的工作，并且确认丢弃，使用-D
```

### 8. 与远程分支同步提交
首先将本地的分支的提交push到远端
```bash
git push --all #--all表示push全部分支，如远端不存在的分支则会自动新建同名分支
```
假设远端做了一些工作，已经合入master分支
```bash
git fetch #抓取远程仓库有，但是本地仓库没有的工作。不会更改HEAD。
git pull #pull=fetch+merge，会将远端的工作和提交与本地merge，如有冲突需要手动解决
git pull --rebase #pull --rebase=fetch+rebase，如有冲突需要手动解决
```

### 9. 将master分支rebase到develop
```bash
git rebase master
```
如果master分支和本地有多个commit冲突，则需要rebase多次，会留下多个rebase commit记录。可以选择对这些重复的rebase commit进行合并
```bash
git rebase -i HEAD~3 #~后面的数字表示HEAD前的第几个commit状态
```
这条命令会进入一个交互界面，修改执行。一般的，第一条保持p，后面的修改为s。

### 10. 将develop分支merge进master
```bash
git checkout master
git merge develop
```

### 11. 将所有本地分支push到远端
```bash
git push --all
```
如果有分支存在冲突，需要先对冲突的分支进行pull（fetch+merge）,然后再进行push