1.输入指令：`git add 文件名称` 或者 `git add .`

2.输入指令：`git commit -m "注释内容"`

3.这一步从本地仓库或本地分支获取并集成(整合)，输入指令：`git pull origin master`

4.如果过程中出现‘please enter a commit message…’,首先按下esc退出键然后输入 ：wq即可

5.输入指令：`git push -u origin master`

按照这些更新步骤走完之后刷新你的 Github 主页就能看到文件已经推送到仓库，从仓库中的文件推送时间就可以知道。

如果你发现文件的推送并不是你此次更新的时间而是上次推送时间，证明你并没有更新成功，请仔细检查再重新敲一遍更新流程即可。