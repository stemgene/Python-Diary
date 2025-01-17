# Github

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Git是具有本地repository的，`git commit`的作用就是推送到本地repository

## 基本git指令

```
git status
git log
# basic
git add .
git commit -m "updata information"
git remote -v
>>>origin	git@github.com:s/exercise.git (fetch)
>>>origin	git@github.com:s/exercise.git (push)
git push origin master
git checkout .    恢复到未submit之前的状态，删除所有修改的操作
```

{% embed url="https://guides.github.com/activities/hello-world/" %}

{% embed url="https://blog.csdn.net/leedaning/article/details/51304690" %}

## Debug

### 嵌套git

当想要提交的文件夹中还嵌有另外的git内容，要么合并在一起，要么删掉其中的一个git。

{% embed url="https://stackoverflow.com/questions/62056294/github-folders-have-a-white-arrow-on-them#:~:text=This%20means%20that%20it%20is,git%20folder." %}

删除的话就进入到这个文件夹，输入`rm -fr .git`，然后退回到想要进行git的文件夹（往往是上层）执行`git rm --cached yourfolder`，再重新`git add .`

## 情景实例

### 恢复到之前的版本

```bash
// 恢复到上一个版本
git restore .

// 恢复到之前某次的版本
// 先查看commit编号
git log --oneline
返回一系列提交的commit，最上面的好像是最近一次提交
87cc56b (HEAD -> main, origin/main, origin/HEAD) update
b344422 finish display and input data
83a156b create filter and empty page
a184b83 display company info
7b8eac1 update
6bffeab initialize

// 方式一：硬重置到指定版本
git reset --hard b344422
// 方式二：保留当前版本，并创建新分支
git checkout -b restore-to-second b344422
// 方式二之后，如果保留restore-to-second这个版本，则先切回master或main，然后merge
git checkout main
git merge restore-to-second
git add .
git commit
git branch -d restore-to-second （可选，删除分支）
// 方式二之后，如果不想保留restore-to-second这个版本，并回到原有的状态，可以切回main，并reset
git checkout main
git reset --hard 87cc56b 原有的状态
git branch -d restore-to-second （可选，删除分支）
```



### 临时堆栈

`git stash`用于将当前的工作进度（未提交的修改）保存到一个临时堆栈中，随后可以在需要的时候恢复这些修改

#### 1. 将当前工作存放到stash

```bash
// 有未提交的修改或文件，可以保存到stach，并将工作目录恢复到上一次提交
git stash
```

