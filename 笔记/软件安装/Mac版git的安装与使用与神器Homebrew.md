# **Mac版git的安装与使用与神器Homebrew**

2018.10.28 12:50 1530浏览



作为程序猿们，肯定知道github，最近有时间，所以记录一下git的安装和使用。

**注意：这是Mac版git的安装和使用哦！**

## 神器Homebrew

安装git之前先给大家介绍一下神器Homebrew，Homebrew简称brew，是Mac OSX上的软件包管理工具，能在Mac中方便的安装软件或者卸载软件。可以说有了它，我们就不必去网上费力去找什么官方下载的了。真心可以少爬好多坑。

#### Homebrew安装

Homebrew的安装非常简单，打开终端,把下面的代码复制上去，回车就行。放心下载，官方的。

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

注意：

- 这个安装有点慢，请耐心等待。
- 上面是官方的安装，但是用这个安装后，在国内你使用Homebrew下载，其速度有点慢 (你们懂得）,所以国内有了 [Homebrew镜像](https://link.jianshu.com/?t=http%3A%2F%2Fwww.zhihu.com%2Fquestion%2F31360766)所以也可以用镜像安装，爱折腾的童鞋可以去试试。

#### Homebrew的使用

Homebrew的使用也很简单，基本三步就够了：

- 搜索软件：brew search 软件名，如brew search wget
- 安装软件：brew install 软件名，如brew install wget
- 卸载软件：brew remove 软件名，如brew remove wget

最后附上[Homebrew的官网](https://link.jianshu.com/?t=http%3A%2F%2Fbrew.sh%2Findex_zh-cn.html)
想更深扒的童鞋可以去看看。

## git的安装

方法一：

- 打开终端，执行下面的命令，通过Homebrew安装Git

```
$ brew install git
```

方法二：

[直接去git官网下载就好](https://link.jianshu.com/?t=http%3A%2F%2Fgit-scm.com%2Fdownloads%2F)

## git的使用

在使用git之前，先了解一下git的传输方式

git是加密传输的，加密方式有SSH和HTTPS两种。这两个方式的区别就是：

使用https url克隆对初学者来说会比较方便，复制https url然后到git Bash里面直接用clone命令克隆到本地就好了，但是每次fetch和push代码都需要输入账号和密码，这也是https方式的麻烦之处。而使用SSH url克隆却需要在克隆之前先配置和添加好SSH key，因此，如果你想要使用SSH url克隆的话，你必须是这个项目的拥有者。否则你是无法添加SSH key的，另外ssh默认是每次fetch和push代码都不需要输入账号和密码，如果你想要每次都输入账号密码才能进行fetch和push也可以另外进行设置。

我们在公司里一般是使用SSH方式的。所以这里着重说一下配置SSH来使用Git

SSH使用的是RSA，非对称加密的方式，所以最重要的是生成SSH密钥

- **生成SSH密钥（很重要）**

查看是否已经有了ssh密钥：

```
cd ~/.ssh
```

创建SSH Key：

```
ssh-keygen -t rsa -C "你的邮箱"
```

然后遇到弹出让你设置密码的直接按3个回车，密码直接为空就行。(如果不怕麻烦，设置密码也可以)
查看你的public key,把里面的一串恶心的东西复制，自己保存一下。

```
cat ~/.ssh/id_rsa.pub
```

- **使用git**

到这里SSH秘钥我们就获取完成了。然后是创建本地仓库然后推到远程仓库，或者从远程仓库拉取我们的代码。在这里也有两种方式：终端命令行和客户端。

客户端推荐Sourcetree，免费的，但是需要注册一个账号。但是注册这个账号非常坎坷，经常是收不到邮件，翻墙了也不好使。当时也是查了好多，解决办法都不好，后来灵机一动，直接用谷歌账号登录就没问题，谷歌账号的注册还是比较容易的，当然也需要翻墙。

图形操作比较简单，所以这里记录一下命令行的操作。将本地的项目放到github上进行管理。

登陆GitHub，打开“Account settings”，然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴你复制的内容。点“Add Key”，你就应该看到已经添加的Key。为了验证是否成功。

```
ssh -T git@github.com
```

如果是第一次的会提示是否continue，输入yes就会看到：You’ve successfully authenticated, but GitHub does not provide shell access 。这就表示已成功连上github。
接下来我们要做的就是把本地仓库传到github上去，在此之前还需要设置username和email，因为github每次commit都会记录他们。

```
git config --global user.name "your name"git config --global user.email "your_email@youremail.com"
```

**注意：这一步我设置好久，不过总是bug，索性我就跳过了，后来也没事，不过大家最好设置一下，通过了更好**

- **命令行上传代码或项目**

1.建立git仓库

cd到你的本地项目根目录下，执行git命令，此命令会在当前目录下创建一个.git文件夹。

```
git init
```

2.将项目的所有文件添加到仓库中

```
git add .
```

这个命令会把当前路径下的所有文件，添加到待上传的文件列表中。
如果想添加某个特定的文件，只需把.换成特定的文件名即可.

3.将add的文件commit到仓库

```
git commit -m "注释语句"
```

4.去github上创建自己的仓库，这个仓库就是用来储存你的代码的，注意拿到创建的仓库的https地址。
5.将本地的仓库关联到github上

```
git remote add origin https://自己的仓库https地址
```

6.上传代码到github远程仓库

```
git push -u origin master
```

执行完后，如果没有异常，等待执行完就上传成功了，中间可能会让你输入Username和Password，你只要输入github的账号和密码就行了.
接下来打开你的github上你建的那个仓库，你就可以看到你代码或项目已经上传上去。

### 使用git的常见错误！

下面就是我爬了好久的坑（-.-）

- **输入git push -u origin master**

出错信息：error:failed to push som refs to …….

解决办法如下：

1、先输入$ git pull origin master //先把远程服务器github上面的文件拉下来。这里可能会出现：

Please enter a commit message to explain why this merge is necessary.
（请输入提交消息来解释为什么这种合并是必要的）

你直接按回车的时候会出现终端编辑界面，让你输入解释，果断不用管！

（1）按键盘左上角”Esc”

（2）输入”:wq”,注意是冒号+wq,按回车键即可

2、再输入$ git push origin master

3、如果出现报错 fatal: Couldn’t find remote ref master或者fatal: ‘origin’ does not appear to be a git repository以及fatal: Could not read from remote repository.

4、则需要重新输入$ git remote add origin [https://自己的仓库https地址](https://link.jianshu.com/?t=https%3A%2F%2Fxn--https-lh2hw31cxdw38dlpbhw0lou2a%2F)

- **如果输入$ git remote add origingit@github.com:djqiang（github帐号名）/gitdemo（项目名）.git**

提示出错信息：fatal: remote origin already exists.
解决办法如下：
1、先输入$ git remote rm origin
2、再输入$ git remote add origin [git@github.com](https://link.jianshu.com/?t=mailto%3Agit%40github.com):djqiang/gitdemo.git 就不会报错了！
3、如果输入$ git remote rm origin 还是报错的话，error: Could not remove config section ‘remote.origin’. 我们需要修改gitconfig文件的内容
4、找到你的github的安装路径
5、找到一个名为gitconfig的文件，打开它把里面的[remote “origin”]那一行删掉就好了！
如果输入$ ssh -T [git@github.com](https://link.jianshu.com/?t=mailto%3Agit%40github.com)
出现错误提示：Permission denied (publickey).因为新生成的key不能加入ssh就会导致连接不上github。
解决办法如下：
1、先输入$ ssh-agent，再输入$ ssh-add ~/.ssh/id_key，这样就可以了。
2、如果还是不行的话，输入ssh-add ~/.ssh/id_key 命令后出现报错Could not open a connection to your authentication agent.解决方法是key用Git Gui的ssh工具生成，这样生成的时候key就直接保存在ssh中了，不需要再ssh-add命令加入了，其它的user，token等配置都用命令行来做。
3、最好检查一下在你复制id_rsa.pub文件的内容时有没有产生多余的空格或空行，有些编辑器会帮你添加这些的。