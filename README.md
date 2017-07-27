# Get-started
From here, you will get almost everything on how to use the Github to control version.
===================

注意事项：
1. 创建仓库时（Create a New Repository），填好名称，务必选择私有库（**Private**），然后Create；
2. 严禁在master分支上直接修改程序；
3. 必须在master分支上创建新的特性分支，并给予直观清楚的名字；
4. 严禁将没有通过测试人员测试的新特性分支版本merge到master分支，除非通过测试人员测试。
 
## 1. Github 安装
- [下载 git OSX 版](http://code.google.com/p/git-osx-installer/downloads/list?can=3)
- [下载 git Windows 版](http://msysgit.github.io/)
- [下载 git Linux 版](http://book.git-scm.com/2_installing_git.html)

## 2. 配置Git
首先在本地创建ssh key；

```
  $ ssh-keygen -t rsa -C "your_email@youremail.com"
```

后面的your_email@youremail.com改为你在github上注册的邮箱，之后会要求确认路径和输入密码，我们这使用默认的一路回车就行。成功的话会在~/下生成.ssh文件夹，进去，打开id_rsa.pub，复制里面的key。

回到github，进入 Account Settings（账户配置），左边选择SSH Keys，Add SSH Key,title随便填，粘贴在你电脑上生成的key。
 
![](http://www.runoob.com/wp-content/uploads/2014/05/github-account.jpg)

为了验证是否成功，在git bash下输入：

```
  $ ssh -T git@github.com
```

如果是第一次的会提示是否continue，输入yes就会看到：You've successfully authenticated, but GitHub does not provide shell access 。这就表示已成功连上github。

接下来我们要做的就是把本地仓库传到github上去，在此之前还需要设置username和email，因为github每次commit都会记录他们。

```
  $ git config --global user.name "your name"
  $ git config --global user.email "your_email@youremail.com"
```

进入要上传的仓库，右键git bash，添加远程地址：

```
  $ git remote add origin git@github.com:yourName/yourRepo.git
```

后面的yourName和yourRepo表示你再github的用户名和刚才新建的仓库，加完之后进入.git，打开config，这里会多出一个remote "origin"内容，这就是刚才添加的远程地址，也可以直接修改config来配置远程地址。

创建新文件夹，打开，然后执行 git init 以创建新的 git 仓库。

## 3. 克隆仓库
执行如下命令以创建一个本地仓库的克隆版本：

```
  git clone username@host:/path/to/repository
```

## 4. 工作流程
你的本地仓库由 git 维护的三棵"树"组成。第一个是你的 工作目录，它持有实际文件；第二个是 暂存区（Index），它像个缓存区域，临时保存你的改动；最后是 HEAD，它指向你最后一次提交的结果。

![](http://www.runoob.com/wp-content/uploads/2014/05/trees.png)
 
**第一步：提出更改（把它们添加到暂存区）：**
```
  git add <filename>
  git add *
```
 
**第二步：提交改动到HEAD：**
 
```
  git commit -m "English infor."
```
 
**第三步：推送改动到远端仓库：**
 
```
  git push origin master
```

可以把 master 换成你想要推送的任何分支。

如果你还没有克隆现有仓库，并欲将你的仓库连接到某个远程服务器，你可以使用如下命令添加：

```
  git remote add origin <server>
```

如此你就能够将你的改动推送到所添加的服务器上去了。

## 5. 分支
分支是用来将特性区分开来的。在你创建仓库的时候，master 是"默认的"分支。在其他分支上进行开发，完成后再将它们合并到主分支上。

![](http://www.runoob.com/wp-content/uploads/2014/05/branches.png)

**第一步：创建一个叫做"feature_x"的分支，并切换过去：**
 
```
  git checkout -b feature_x
```
 
**第二步：切换回主分支：**
 
```
  git checkout master
```
 
**第三步：再把新建的分支删掉：**
 
```
  git branch -d feature_x
```
 
可以将分支推送到远端仓库，此分支可以作为新的特征版本供他人协同使用：
 
```
  git push origin <branch>
```

## 6. 更新与合并
**一：获取最新版本，将远端的最新版本更新至本地仓库：**

```
  git pull
```

以在你的工作目录中 获取（fetch） 并 合并（merge） 远端的改动。

**二：合并其他分支到你的当前分支（例如 master）：**
 
```
  git merge <branch>
```

在这两种情况下，git 都会尝试去自动合并改动。遗憾的是，这可能并非每次都成功，并可能出现冲突（conflicts）。 这时候就需要你修改这些文件来手动合并这些冲突（conflicts）。改完之后，你需要执行如下命令以将它们标记为合并成功：

```
  git add <filename>
```

**三：在合并改动之前，你可以使用如下命令预览差异：**
 
```
  git diff <source_branch> <target_branch>
```

## 7. 标签
**软件发布之前必须创建标签。**

通过如下命令创建一个叫做 1.0.0 的标签：
 
```
  git tag 1.0.0 1b2e1d63ff
```

1b2e1d63ff 是你想要标记的提交 ID 的前 10 位字符。可以使用下列命令获取提交 ID：

```
  git log
```

你也可以使用少一点的提交 ID 前几位，只要它的指向具有唯一性。

## 8. 替换本地改动
假如你操作失误，你可以使用如下命令替换掉本地改动：

```
  git checkout -- <filename>
```

此命令会使用 HEAD 中的最新内容替换掉你的工作目录中的文件。已添加到暂存区的改动以及新文件都不会受到影响。

假如你想丢弃你在本地的所有改动与提交，可以到服务器上获取最新的版本历史，并将你本地主分支指向它：

```
  git fetch origin
  git reset --hard origin/master
```

## 9. 链接与资源
### 9.1. 图形化客户端
- [GitX (L) (OSX, 开源软件)](http://gitx.laullon.com/)
- [Tower (OSX)](http://www.git-tower.com/)
- [Source Tree (OSX, 免费)](http://www.sourcetreeapp.com/)
- [GitHub for Mac (OSX, 免费)](http://mac.github.com/)
- [GitBox (OSX, App Store)](https://itunes.apple.com/gb/app/gitbox/id403388357?mt=12)

### 9.2. 指南和手册
- [Git 社区参考书](http://book.git-scm.com/)
- [专业 Git](http://progit.org/book/)
- [像 git 那样思考](http://think-like-a-git.net/)
- [GitHub 帮助](http://help.github.com/)
- [图解 Git](http://marklodato.github.io/visual-git-guide/index-zh-cn.html)

### 9.3. 相关文章
- [Github 简明指南](http://rogerdudler.github.io/git-guide/index.zh.html)
- [如何高效利用GitHub](http://www.yangzhiping.com/tech/github.html)

## END

> 内容引自：http://www.runoob.com/w3cnote/git-guide.html
