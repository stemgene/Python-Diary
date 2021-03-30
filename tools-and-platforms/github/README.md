# Github

## 关联本地文件夹

参考：[https://help.github.com/cn/github/authenticating-to-github/connecting-to-github-with-ssh](https://help.github.com/cn/github/authenticating-to-github/connecting-to-github-with-ssh)

1.在github网站新建一个repository

![](../../.gitbook/assets/image%20%2810%29.png)

2. 进入本机想要关联的文件夹，然后依次输入

```text
git init
git add .
git commit -m 'First commit'
```

3. 复制repository的URL

![](../../.gitbook/assets/image%20%2826%29.png)

4. 添加URL地址到本地文件夹的git中

```text
git remote add origin 刚才的url
git remote -v
```

5. 生成ssh key

```text
ssh-keygen -t rsa -C "github邮箱" -b 4096 -f ~/.ssh/id_rsa_github
# add key to ssh-key chain
#有时候，会提示没有public key，此时需要重新配置一下config文件
ssh-add -K ~/.ssh/id_rsa_github
```

6. edit config文件

```text
Host InsightDS
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa_github
```

```text
chmod 600 ~/.ssh/config
```

7. 将public key上传到github中，在setting中有SSH配置选项，添加public key

![](../../.gitbook/assets/image%20%2831%29.png)

8. 测试联通情况

```text
ssh -T git@github.com
git push -u origin master
```

此时就可以正常push本地文件到github上了。

## 基本git指令

```text
git status
git log
# basic
git add .
git commit -m "updata information"
git remote -v
>>>origin	git@github.com:s/exercise.git (fetch)
>>>origin	git@github.com:s/exercise.git (push)
git push origin master
```

[https://guides.github.com/activities/hello-world/](https://guides.github.com/activities/hello-world/)



