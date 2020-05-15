# 填坑

## Python环境

### Bug：vscode找不到文件

在使用`open()`函数时，明明txt文件和py文件在同一个目录下，如果使用相对路径来打开的话，可以直接在open函数中使用txt文件名，可是在vscode中确一直报错，因为vscode的当前路径可能并不是这个py文件的路径，只有vscode的当前路径和py路径一致时，才可以直接使用txt文件名来打开！

解决办法：找到文件的relative path。可以通过os.path或者通过vscode自身的功能。参考：[https://www.cnblogs.com/wjw2018/p/10536355.html](https://www.cnblogs.com/wjw2018/p/10536355.html)

