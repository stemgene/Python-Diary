---
description: >-
  参考视频：https://www.bilibili.com/video/BV1p7411d7Fv/?spm_id_from=333.337.search-card.all.click&vd_source=81884c519d60bbdad4b6fd87d340415f
---

# Pull Request

[https://www.bilibili.com/video/BV1s3411g7PS/?spm\_id\_from=333.337.search-card.all.click\&vd\_source=81884c519d60bbdad4b6fd87d340415f](https://www.bilibili.com/video/BV1s3411g7PS/?spm\_id\_from=333.337.search-card.all.click\&vd\_source=81884c519d60bbdad4b6fd87d340415f)

想要参与到open source项目中，需要和整体项目进行融合，需要熟练掌握Pull Request的操作。

利用两个账号实验pull request

#### Step 0：查看状态，切换本地账号

```
// 查看local配置文件
git config --list
// 主账号
user.name=Haoyuan Dong
user.email=hlj...
// 小号
user.name=stemgene-bot
user.email=music....
```

不需要设置global变量，先clone到本地，进入文件夹后可以设置局部变量

```
// Some code
git config user.name "name"
git config user.email "email"
```

### 整体过程

想要参与到项目中，应该fork项目到自己的github中，而不是直接clone源项目

目标项目名称为heat，所有者codeforboston，我的github账号stemgene

1. 在github上fork目标项目到stemgene的账号上
2. clone stemgene/heat到我的本地电脑上：

```
git clone https://github.com/stemgene/heat.git
```

3. 添加源项目作为上游仓库，以便能够同步源项目的更新：

```
git remote add upstream https://github.com/codeforboston/heat.git
```

4. 创建branch:&#x20;

```
git checkout -b opt/rename_classes
```

5. 修改代码
6. 修改之后同步源项目的更新：git fetch upstream确保codeforboston/heat的代码是最新的

* 分开fetch和merge，避免可能发生的复杂情况

```
git checkout main   # 切换到本地分支
git fetch upstream
git merge upstream/main 注意如果源项目使用的是master分支，需要将main替换为master
git checkout opt/rename_classes #切回工作分支
git rebase main  #将main分支的最新更改应用到工作分支
```

* 使用pull（pull可以理解为fetch & merge的双重操作)更快捷

```
git checkout main
git pull upstream main #将源项目（upstream）的 main 分支的更新拉取并合并到本地的 main 分支。
git checkout opt/rename_classes   # 切换回你的工作分支
git pull --rebase origin main #将本地 main 分支的更改合并到你的工作分支（如 rename_classes）
```

7. 提交到自己的repository中：git add . -> git commit -m "update" -> git push

```
git add .
git commit -m "rename two classes"
git push origin opt/rename_classes
```

7. 在自己的仓库 `stemgene/heat` 中，切换到刚推送的 opt/`rename_classes` 分支。点击 **Compare & pull request** 按钮，填写Pull Request的标题和描述，并提交Pull Request，等待项目维护者审查。
