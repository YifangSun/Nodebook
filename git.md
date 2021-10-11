
## 远程
### 删除远程分支
查看所有分支：
```shell
git branch -a
```
然后选择删除
```shell
git push origin --delete new_a
```

### 查看remote

```shell
git remote -v
```

## 本地

### 更换源

```shell
git commit -m "Change repo." # 先把所有为保存的修改打包为一个commit
git remote remove origin # 删掉原来git源
git remote add origin [YOUR NEW .GIT URL] # 将新源地址写入本地版本库配置文件
git push -u origin master # 提交所有代码
```

### 查看diff

查看未添加add：

git diff

查看已经add但未commit：

git diff --cached

### 更新commit

git rebase -i [sha256]

把要编辑的提交信息从pick改成edit，然后

git commit --amend

改完再

git rebase --continue

### 合并修改历史

`git rebase -i [sha256]` 或者`git rebase -i HEAD~3`

然后弹出的窗口中需要保留的提交保留pick, 需要合并掉的改为s或者f。:wq保存。

再弹出一个窗口修改commit信息，改完或者直接:wq。

然后如果只有一个pick，本次rebase就直接完成。否则分支名字会变成dev_c14 | REBASE 3/5。

`git rebase --skip`或`git rebase --continue`完成修改，可以提交了。

`git push --force origin dev_c14:test`强行提交。

### 强行更新

**强行更新到最新**

```
git fetch --all
git reset --hard origin/master
```

git fetch 只是下载远程的库的内容，不做任何的合并 git reset 把HEAD指向刚刚下载的最新的版本

### 重命名

```shell
git branch -m oldName newName
```

### 删除分支

```shell
git branch -d syf 
```

### 拉新分支

**拉远程分支到本地新分支**

```shell
方法1：
# 可以把远程某个分支remote_branch_name拉去到本地的branch_name下，如果没有branch_name，则会在本地新建branch_name
git fetch origin remote_branch_name:branch_ame
# 然后切换分支
git checkout branch_name

方法2：
# 获取远程分支到本地，并切换分支
git checkout -b branch_name remotes/origin/remote_branch_name
```
### 撤销

**撤销文件修改**

https://blog.csdn.net/weixin_31826879/article/details/113566281

## 综合

### 设置用户名、邮箱

```shell
git config --list
git config --global user.name "xxx"
git config --global user.email "xxx@x.com"
```

https://www.cnblogs.com/heqiyoujing/p/10722414.html

