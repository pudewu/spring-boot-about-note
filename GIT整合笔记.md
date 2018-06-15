# Git上传和常用命令

## 1  配置Git 

我们先在电脑硬盘里找一块地方存放本地仓库，比如我们把本地仓库建立在C:\MyRepository\1ke_test文件夹下

进入1ke_test文件夹 鼠标右键操作如下步骤：

### 1）在本地仓库里右键选择Git Init Here，会多出来一个.git文件夹，这就表示本地git创建成功。右键Git Bash进入git命令行，截图效果如下： 

为了保险起见，我们先执行git init命令

```java
$ git init
```

![img](http://1ke.co/files/course/2015/06-10/18283539cfad664272.png?4.9.3) 

为了把本地的仓库传到github，还需要配置ssh key。 

### 2）在本地创建ssh key

```
$ ssh-keygen -t rsa -C "your_email@youremail.com"
```

后面的your_email@youremail.com改为你的邮箱。我的邮箱是lilu@1ke.co，也是在github上注册的那个邮箱：

![img](http://1ke.co/files/course/2015/06-10/18094049ed5a347715.png?4.9.3) 

直接点回车，说明会在默认文件id_rsa上生成ssh key。 

重复密码时也是直接回车，之后提示你shh key已经生成成功。 

![img](http://1ke.co/files/course/2015/06-10/1811142d4ce9788031.png?4.9.3) 

然后我们进入提示的地址下查看ssh key文件。 我的电脑的地址是C:\Users\Administrator\.ssh ，其中lilu是我的电脑的名称 

![1528867365403](C:\Users\Administrator\AppData\Local\Temp\1528867365403.png)

打开id_rsa.pub，复制里面的key。里面的key是一对看不懂的字符数字组合，不用管它，直接复制。 

回到github网站，进入Account Settings，左边选择SSH Keys，Add SSH Key, 

![img](http://1ke.co/files/course/2015/06-10/18040663f13e163573.png?4.9.3) 

title随便填，粘贴key 

![img](http://1ke.co/files/course/2015/06-10/18124918c556633334.png?4.9.3) 

### 3）验证是否成功，在git bash下输入 

```
$ ssh -T git@github.com
```

回车就会看到：You’ve successfully authenticated, but GitHub does not provide shell access 。这就表示已成功连上github。 

![img](http://1ke.co/files/course/2015/06-10/18141358d223257547.png?4.9.3) 

### 4）接下来我们要做的就是把本地仓库传到github上去，在此之前还需要设置username和email，因为github每次commit都会记录他们 

```cmd
$ git config --global user.name "your name"
$ git config --global user.email "your_email@youremail.com"
```

分别输入上述命令行 回车， 我的界面显示如下 

![img](http://1ke.co/files/course/2015/06-10/1816524de546595658.png?4.9.3) 

### 5）进入要上传的仓库，右键git bash，添加远程地址 

```cmd
$ git remote add origin git@github.com:yourName/yourRepo.git
```

后面的yourName和yourRepo表示你再github的用户名和刚才新建的仓库，加完之后进入.git，打开config，这里会多出一个remote “origin”内容，这就是刚才添加的远程地址，也可以直接修改config来配置远程地址。 

![img](http://1ke.co/files/course/2015/06-10/1823037aa1ed043887.png?4.9.3) 

## 2 提交上传 

### 1）接下来在本地仓库里添加一些文件，比如README 

在本地新建一个README文件 

![img](http://1ke.co/files/course/2015/06-10/183003b8e527974368.png?4.9.3) 

然后在命令行输入一下命令 

```cmd
$ git add README

$ git commit -m "first commit"
```

![img](http://1ke.co/files/course/2015/06-10/183203309ad2517953.png?4.9.3) 

### 2）上传到github  

```cmd
$ git push origin master
```

git push命令会将本地仓库推送到远程服务器。

git pull命令则相反。

注：首次提交，先git pull下，修改完代码后，使用git status可以查看文件的差别，使用git add 添加要commit的文件。



## 3 Git命令 

查看、添加、提交、删除、找回，重置修改文件 

```cmd
git help <command> # 显示command的help

git show # 显示某次提交的内容 git show $id

git co -- <file> # 抛弃工作区修改

git co . # 抛弃工作区修改

git add <file> # 将工作文件修改提交到本地暂存区

git add . # 将所有修改过的工作文件提交暂存区

git rm <file> # 从版本库中删除文件

git rm <file> --cached # 从版本库中删除文件，但不删除文件

git reset <file> # 从暂存区恢复到工作文件

git reset -- . # 从暂存区恢复到工作文件

git reset --hard # 恢复最近一次提交过的状态，即放弃上次提交后的所有本次修改

git ci <file> git ci . git ci -a # 将git add, git rm和git ci等操作都合并在一起做　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　git ci -am "some comments"

git ci --amend # 修改最后一次提交记录

git revert <$id> # 恢复某次提交的状态，恢复动作本身也创建次提交对象

git revert HEAD # 恢复最后一次提交的状态
```

查看文件diff 

```cmd
git diff <file> # 比较当前文件和暂存区文件差异 git diff

git diff <id1><id2> # 比较两次提交之间的差异

git diff <branch1>..<branch2> # 在两个分支之间比较

git diff --staged # 比较暂存区和版本库差异

git diff --cached # 比较暂存区和版本库差异

git diff --stat # 仅仅比较统计信息
```

查看提交记录 

```cmd
git log git log <file> # 查看该文件每次提交记录

git log -p <file> # 查看每次详细修改内容的diff

git log -p -2 # 查看最近两次详细修改内容的diff

git log --stat #查看提交统计信息
```

Git 本地分支管理 查看、切换、创建和删除分支 

```cmd
git br -r # 查看远程分支

git br <new_branch> # 创建新的分支

git br -v # 查看各个分支最后提交信息

git br --merged # 查看已经被合并到当前分支的分支

git br --no-merged # 查看尚未被合并到当前分支的分支

git co <branch> # 切换到某个分支

git co -b <new_branch> # 创建新的分支，并且切换过去

git co -b <new_branch> <branch> # 基于branch创建新的new_branch

git co $id # 把某次历史提交记录checkout出来，但无分支信息，切换到其他分支会自动删除

git co $id -b <new_branch> # 把某次历史提交记录checkout出来，创建成一个分支

git br -d <branch> # 删除某个分支

git br -D <branch> # 强制删除某个分支 (未被合并的分支被删除的时候需要强制)
```

 分支合并和rebase 

```cmd
git merge <branch> # 将branch分支合并到当前分支

git merge origin/master --no-ff # 不要Fast-Foward合并，这样可以生成merge提交

git rebase master <branch> # 将master rebase到branch，相当于： git co <branch> && git rebase master && git co master && git merge <branch>
```

Git远程仓库管理 

```cmd
git remote -v # 查看远程服务器地址和仓库名称

git remote show origin # 查看远程服务器仓库状态

git remote add origin git@ github:robbin/robbin_site.git # 添加远程仓库地址

git remote set-url origin git@ github.com:robbin/robbin_site.git # 设置远程仓库地址(用于修改远程仓库地址) git remote rm <repository> # 删除远程仓库
```

