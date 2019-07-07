# [Mac brew安装redis](https://www.cnblogs.com/ihuangjianxin/p/9390650.html)



1、安装redis

```
`$ brew install redis`
```

　　![img](http://ww2.sinaimg.cn/large/006tNc79ly1g4rwf07ru5j318q0hydk2.jpg)

 

Error：Failed to download resource "reds"  // 下载reds失败

不过不需要担心，brew会已经从其它地方下载并正确安装了

 

**配置文件路径： /usr/local/etc/redis.conf**

 

 

2、启动redis（可选）

```
$ redis-server
```

3、添加至开机启动项（可选）

```
$ ln -f /usr/local/Cellar/redis/2.8.13/homebrew.mxcl.redis.plist ~/Library/LaunchAgents/
$ launchctl load ~/Library/LaunchAgents/homebrew.mxcl.redis.plist
```