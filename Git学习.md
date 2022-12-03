# Git初始化、配置、设置密钥

```
git init #初始化该文件夹为git目录
git config --global user.name "Rikasai_home" #设置本地git的用户名，推送到远程的时候能查看到
git config --global user.email "lihuacai168@gmail.com" #设置邮箱
ssh-keygen -t rsa -C "lihuacai168@gmail.com" #生成密钥，路径是: /c/Users/本地用户/.ssh
cat id_rsa.pub #查看id_rsa.pub的内容，复制这段内容放在远程账号Settings/SSH and GPG keys；如果没有则会出现：Permission denied (publickey)
```

# Git增加，提交，查看，撤销

```
git add a.txt #把在工作区增加新的文件暂存区（stage）
git commit -m "creat a.txt" #提交a.txt文件提交到当前的分支
git diff #查看被修改的具体内容
git diff HEAD -- a.txt #命令可以查看工作区和版本库里面最新版本的区别
git reset HEAD a.txt #可以把暂存区的修改撤销掉（unstage），重新放回工作区
git checkout -- a.txt #丢弃工作区的修改
```

# Git查看log 回退版本

```
git log #查看gitcommit的记录，时间是由近到远
git log --pretty=oneline #加上 --pretty=oneline 会只显示commit id和 commit -m的内容
git reset --hard HEAD^ #hard HEAD^回退到上一个版本，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100
git reflog #查看历史的每一次记录
git reset --hard f91ed98 #回退到指定的版本
```

# 绑定Git远程仓库，拉去，推送

```
git remote add origin git@github.com:lihuacai168/docker.git #关联远程仓库，origin是远程仓库名字在本地的名字,lihuacai168是github用户名，docker.git远程仓库的真是名字
git fetch #从远程获取最新代码，但不切换
git branch 查看当前HEAD指向的分支
git branch a #创建a分支
git checkout a#切换到a分支
git checkout af34sdl#切换到af34sdl这次提交的代码
git pull origin master --allow-unrelated-histories #解决refusing to merge unrelated histories
git push origin master #本地的master分支推送到远程的master分支，因为两者已经关联，才能这样操作。实际上是 git push origin master:master
```


# git rebase
- 从master新建feat-1分支
- feat-1分支提交一个commit
- feat-2分支提交一个commit, pull request, rebase and merge并且到master
- feat-1分支提交一个commit
- master分支update
- feat-1分支上rebase feat-1 onto master
- pull request, rebase and merge并且到master
- 最终feat-1和feat-2分支的每一个commit都会被复制一份到master上，commit id会变
- ![](https://cdn.jsdelivr.net/gh/lihuacai168/images/img/202212031310201.png)
- ![](https://cdn.jsdelivr.net/gh/lihuacai168/images/img/202212031406370.png)


# git merge
- 从master新建feat-3分支
- feat-3分支提交一个commit
- > feat-4分支提交一个commit, pull request, merge并且到master  
  > 在master上会产生一个Merge pull request #4的commit
  > ![](https://cdn.jsdelivr.net/gh/lihuacai168/images/img/202212031434164.png)
- feat-3分支提交一个commit
- master分支update
- > merge master to feat-3  
  > 在feat-3上会产生一个Merge branch 'master' into feat-3的commit
  > ![](https://cdn.jsdelivr.net/gh/lihuacai168/images/img/202212031441847.png)
- > pull request, merge并且到master  
  > 在master上会产生一个Merge pull request #5的commit
  > ![](https://cdn.jsdelivr.net/gh/lihuacai168/images/img/202212031443990.png)

# diff-rebase-merge
- ![](https://cdn.jsdelivr.net/gh/lihuacai168/images/img/202212031453976.png)
