## 合并修改历史

git rebase -i [sha256] 或者git rebase -i HEAD~3

然后弹出的窗口中需要保留的提交保留pick, 需要合并掉的改为s或者f。:wq保存。

再弹出一个窗口修改commit信息，改完或者直接:wq。

然后分支名字会变成dev_c14 | REBASE 3/5

git rebase --skip可以完成修改，可以提交了。

git push --force origin dev_c14:test