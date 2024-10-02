改**git push**的的时候用到的用户信息。

方式一：对于windows系统， 选择控制面板-》凭据管理器-》windows凭据，删除里面类似git相关的的用户信息。下图中以git打头的相关数据。 这样你在敲git push就会弹出对话框让你重新输入用户名和密码。 输入你要更改的用户名和密码就可以了哦。

![](https://pic2.zhimg.com/80/v2-4e374f671ae1933035ced93a55299fb9_1440w.webp)

方式二：修改你本地git仓库里面的config文件。目录位于 **.git** -》config 文件 。在url前面手动输入用户名和密码 格式为 http\://或者[https://username](https://link.zhihu.com/?target=https%3A//username)\:userpassword@具体的仓库地址(这里不要写协议名称，就是http，htthps). 示例 [https://test](https://link.zhihu.com/?target=https%3A//test):[http://testpasswd](https://link.zhihu.com/?target=http%3A//testpasswd)@gitlab.test.com/test.git

![](https://pic4.zhimg.com/80/v2-348800b6798f48505b279a52c6b3745b_1440w.webp)

。

使用方式二， 就不用删除控制面板里面的用户凭证，但只会影响一个git仓库，不会影响全体git仓库。 方式一会影响所有git仓库。

使用方式二，如果用户密码有特殊字符，需要进行url编码。附常用符号编码

| 字符   | URL编码 |
| :--- | :---- |
| （空格） | %20   |
| "    | %22   |
| #    | %23   |
| %    | %25   |
| &    | %26   |
| (    | %28   |
| )    | %29   |
| +    | %2B   |
| ,    | %2C   |
| /    | %2F   |
| :    | %3A   |
| ;    | %3B   |
| <    | %3C   |
| =    | %3D   |
| >    | %3E   |
| ?    | %3F   |
| @    | %40   |
| \\   | %5C   |
| \|   | %7C   |

[git切换用户、多用户切换的正确方式 git commit和git push 切换用户 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/345915480)
