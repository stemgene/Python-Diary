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
