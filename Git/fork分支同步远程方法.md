fork别人的项目clone到本地后，远程分支有修改，需要同步远程分支，使得本地代码与远程分支一致。
1. git remote -v:

orgin：为本地分支的

upstream：为远程分支

2. git remote add upstream <原作者项目的URL>（上一步操作没有upstream，则需要添加uptream）
完成后，执行git remote -v确认与上图一致。

3. git fetch upstream 将远程分支同步到本地

4. git checkout master 检查本地代码变更

5. git merge upstream/master 合并分支
