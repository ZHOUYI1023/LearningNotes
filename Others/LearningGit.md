git checkout -- readme.txt
把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
* 一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
* 一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
总之，就是让这个文件回到最近一次git commit或git add时的状态。

---

git reset HEAD readme.txt
把暂存区的修改回退到工作区。

---

git reset --hard commit_id
git reset --hard HEAD^
git reset --hard HEAD~1 # 删除本地最后一条记录，如果需要删除最后提交的N条记录，将“1”替换为一个具体的数字“N”即可。
当前版本回退到某一个/上一个版本

---

git rebase -i a8547 # 最后一条待删除记录的前(时间上)一条记录ID

---

checkout (switch to) target branch.
git cherry-pick <commit id>
