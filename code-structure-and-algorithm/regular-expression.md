# Regular Expression

从简单的例子开始：如果直接给出字符，就是精确匹配，用`\d`可以匹配一个数字，`\w`可以匹配一个字母或数字，所以：

* `'00\d'`可以匹配`'007'`，但无法匹配`'00A'`；
* `'\d\d\d'`可以匹配`'010'`；
* `'\w\w\d'`可以匹配`'py3'`；

`.`可以匹配任意字符，所以：

* `'py.'`可以匹配`'pyc'`、`'pyo'`、`'py!'`等等。

要匹配变长的字符，在正则表达式中，用`*`表示任意个字符（包括0个），用`+`表示至少一个字符，用`?`表示0个或1个字符，用`{n}`表示n个字符，用`{n,m}`表示n-m个字符：

来看一个复杂的例子：`\d{3}\s+\d{3,8}`。

我们来从左到右解读一下：

1. `\d{3}`表示匹配3个数字，例如`'010'`；
2. `\s`可以匹配一个空格（也包括Tab等空白符），所以`\s+`表示至少有一个空格，例如匹配`' '`，`' '`等；
3. `\d{3,8}`表示3-8个数字，例如`'1234567'`。

综合起来，上面的正则表达式可以匹配以任意个空格隔开的带区号的电话号码。

如果要匹配`'010-12345'`这样的号码呢？由于`'-'`是特殊字符，在正则表达式中，要用`'\'`转义，所以，上面的正则是`\d{3}\-\d{3,8}`。

但是，仍然无法匹配`'010 - 12345'`，因为带有空格。所以我们需要更复杂的匹配方式。

要做更精确地匹配，可以用`[]`表示范围，比如：

* `[0-9a-zA-Z\_]`可以匹配一个数字、字母或者下划线；
* `[0-9a-zA-Z\_]+`可以匹配至少由一个数字、字母或者下划线组成的字符串，比如`'a100'`，`'0_Z'`，`'Py3000'`等等；
* `[a-zA-Z\_][0-9a-zA-Z\_]*`可以匹配由字母或下划线开头，后接任意个由一个数字、字母或者下划线组成的字符串，也就是Python合法的变量；
* `[a-zA-Z\_][0-9a-zA-Z\_]{0, 19}`更精确地限制了变量的长度是1-20个字符（前面1个字符+后面最多19个字符）。

`A|B`可以匹配A或B，所以`(P|p)ython`可以匹配`'Python'`或者`'python'`。

`^`表示行的开头，`^\d`表示必须以数字开头。

`$`表示行的结束，`\d$`表示必须以数字结束。

你可能注意到了，`py`也可以匹配`'python'`，但是加上`^py$`就变成了整行匹配，就只能匹配`'py'`了。





{% embed url="https://blog.csdn.net/yinglang19941010/article/details/52076995" %}

{% embed url="https://blog.csdn.net/tp7309/article/details/72823258" %}

{% embed url="https://www.liaoxuefeng.com/wiki/1016959663602400/1017639890281664" %}

{% embed url="https://segmentfault.com/a/1190000019277109" %}

[https://www.jianshu.com/p/147fab022566](https://www.jianshu.com/p/147fab022566)

[https://www.w3cschool.cn/python3/python3-reg-expressions.html](https://www.w3cschool.cn/python3/python3-reg-expressions.html)

## JavaScript中的正则

{% embed url="https://blog.csdn.net/guanmao4322/article/details/88389200" %}

正则表达式匹配从指定字符开始到指定字符结束的字符串

1.  a.\*?b就是a开始b结束的匹配
2. 如果要限制是一行的开头和末尾的话，就是^a.\*?b$

```text
var phrase = "yesthisismyphrase=thisiswhatIwantmatched"; 
var myRegexp = /phrase=(.*)/;
var match = myRegexp.exec(phrase);
alert(match[1]);
```

```text
var str = 'http://zhipur.com/item?data=SN120180525FEOCE'; 
var code1 = str.match(/\?data=(.*)/)[1];//取 ?data=后面所有字符串
var code2 = str.match(/data=(.*)/)[1];//取 data=后面所有字符串
var code3 = str.match(/data=(.*)/)[0]; //取 包含 data=及后面的字符串
console.log('?data= 后的内容为: '+code1);
console.log('data= 后的内容为: '+code2);
console.log('包含 data= 的所有内容为: '+code3);
```

正则匹配之后返回是一串array，需要用\[0\]或\[1\]等选择具体的内容

