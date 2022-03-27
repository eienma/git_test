### 本地仓库

a. `git init` 在本地创建一个Git仓库；

b. 在本地仓库中添加需要上传的文件；

c. 可以用 `git status` 查看当前的状态

d. `git add .` 将所有项目添加到暂存区；

e. `git commit -m "注释内容"` 将项目提交到Git仓库；

#### Q1 暂存区撤回文件？

比如我不小心把依赖包文件夹node_modules（这个很大而且没必要git管理这份代码）add了，怎么撤回这个文件？

第一种方法：

`git reset HEAD -- node_modules`
注意：双杠--后面有一个空格，后面再跟文件名。

第二种方法：

`git rm -r --cached node_modules`

#### Q2 通过.gitignore排除文件？

Git提供了忽略文件 .gitignore，当我们用`git add . ` 时，Git会自动排除.gitignore文件里匹配到的文件。

在当前文件夹新建一个后缀名为 .gitignore 的文件，用记事本打开该文件，将node_modules填进去，这样，我们执行`git add .` 就不会把node_modules文件包含进去。

### 远程仓库

a. 添加SSH KEY；

由于本地Git仓库和Github仓库之间的传输是通过SSH加密的，所以连接时需要两边都有SSH KEY。

创建之前先看看你的电脑有没有创建过SSH KEY。先看一下你C盘用户目录下有没有.ssh目录，有的话里面有没有id_rsa和id_rsa.pub这两个文件，有就跳到下一步，没有就通过下面命令创建

`ssh-keygen -t rsa -C "email@example.com"`

然后一路回车。这时你就会在用户下的.ssh目录里找到id_rsa和id_rsa.pub这两个文件。登录Github,找到右上角的图标，打开点进里面的Settings，再选中里面的SSH and GPG KEYS，点击右上角的New SSH key，然后Title里面随便填，再把刚才id_rsa.pub里面的内容**全部复制**到Title下面的Key内容框里面，最后点击Add SSH key，这样就完成了SSH Key的加密。

b. 在 GitHub 新建 repositories；建议不勾选`Initialize this repository with a README`

### 本地仓库

a. `git remote add origin git@github.com:UserName/projectName.git` 将本地仓库与远程仓库关联；这里用`remote add`命令添加，`origin`为这个SSH地址的别名，`git@github.com:UserName/projectName.git`为新建的github仓库地址。`remote rm`命令则是删除一个已经存在的地址。

b. `git push -u origin master` 将本地项目推送到远程仓库。

由于新建的远程仓库是空的，所以要加上-u这个参数，等远程仓库里面有了内容之后，下次再从本地库上传内容的时候只需执行：

`git push origin master`

或者可以更简单的：`git push`

当然，这样会默认推送到主支干master。

#### Q3 仓库不为空？

如果在新建一个Github仓库时，选择了

`Initialize this repository with a README`（就是创建仓库的时候自动给你创建一个README.md文件），那么在push的时候，会报错：

```bash
error: failed to push some refs to  https://github.com/BNK-ALONG/teach-design-platform.git
```

这是因为新建的 Github 仓库的 README.md 文件不在本地仓库的目录中，这是问题其实在多人协作开发中是一定存在的，多个人共同关联一个远程仓库，在把你本地的修改上传（push）之前，要把别人的代码更新到自己的本地仓库，不然怎么达到协作开发呢？

将远程仓库最新的更新拉取到本地，并合并到主支干：

`git pull --rebase origin master`

这时再重新push就可以成功了。

#### Q4 删除文件?

`git remote add origin git@github.com:UserName/projectName.git`
`git rm delete.txt`
`git rm ./samples/delete.txt`
`git commit -m "delete test"`
`git push origin master`