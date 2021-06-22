# 科学上网指南（限定版）

## 以下针对Windows版本

### 菜单解析

#### 系统代理模式:

分为三种，**直连模式** ，**pac模式** ， **全局模式** 。  

**直连模式** 就是不通过代理服务器，想当于没有开启这个软件。  

**pac模式** 就是通过一个本地的名单规则来过滤网址，开启此模式后，只有在名单上的网址才会通过代理，该文件在根目录下。 

**全局模式** 就是所有流量都走代理，一般情况下不要一直开这个模式，除非你不确定需要代理的流量地址，或者需要代理的网址不在pac名单上。

#### PAC:

这个菜单是对pac名单的更新操作，由于众所周知的原因，尽量不要用这个菜单内的更新功能。不过可以从这个菜单快速访问pac名单所在的文件夹。

#### 代理规则:

一般情况下，选择 **绕过局域网和大陆**。  

字面意思就是大陆地区的ip都不走代理。选择此项后，在 **pac模式** 下，即使把大陆常见地址加入pac名单，该网址也不会走代理。  

判断是否是大陆ip是通过根目录的 **chn_ip.txt** 来确定的，该文件规则是通过定义两个ip地址，在中间的ip都为大陆ip。

如果选择 **全局模式** ，则代理规则无效，默认全走代理，优先级最高。

**优先级：** 全局模式 > chn_ip > pac

#### 服务器：

现在基本都是用机场了，在这里切换当前连接的节点，一般不要主动编辑服务器信息。

这个菜单下有一个连接统计，可以查看节点是否已经挂掉。

一般情况下，优先使用香港节点，其次是日本，最后是新加坡。

很多机场会提供多倍流量，比如十倍，意思是使用了1MB, 扣除10MB流量。

#### 服务器订阅：

在服务器订阅设置里输入订阅地址，即可出现服务器列表。

类似于 **https://sub.sdfXXXXXXXXXXXXXX.xyz/link/XXXXXXXXXXXX?sub=1** 。  

每次开启SSR会自动更新订阅（可关闭），默认通过代理服务器来更新，如果更新失败，就要手动选择 **更新SSR服务器订阅（不通过代理）** ，此行为也可以解决大部分连接失败的问题。

#### 服务器负载均衡：

在菜单 **选项设置** 里可以选择负载均衡的类型，不过这个功能不太好用，大部分时候节点挂了手动切换比他自己找节点要快。

#### 选项设置：

这里可能用到的有   

**本地端口**，可以更改本地代理的端口，防止冲突，有时候会弹出来端口信息错误的bug，这这里修改一下端口就行。

**开机启动**， 如果机场很稳定可以开启选项。

**开启日志**， 尽量开启。

#### 帮助：

**显示日志**：这个功能很重要，是判断问题所在的主要手段。在这里可以确认是节点挂了，还是地址根本没走代理。还有访问一些链接复杂的外国网站，必须用这个日志记录地址，加入pac名单。

### 错误排查

#### 无法翻墙：

可以在cmd中使用命令 ``ipconfig/flushdns`` 刷新缓存，再重新访问。

多换几个节点。

更新服务器订阅。

关闭软件，重新打开。

#### 网址打不开或下载缓慢：

打开全局模式。

### pac规则

pac文件采用通配符的格式

```text
  "||github.com",
  "||githubusercontent.com",
  "||forexample.com",

```

不要用中文输入法，切换到英文模式。 **||** 适用于匹配开头，形如 **||google.com** ，则表示以 **任意内容 + google.com + 任意内容** 都会触发代理规则，如果要增加自己的常用网站规则，这样写上去就行了，不要忘记了句尾逗号。

pac文件可以参考 ``https://github.com/xfcycc/pac/blob/main/pac.txt``

### 简单的捕捉流量地址的方法

开启日志，开启全局代理，关闭无关软件，再访问网址，一般会出现如 **Connect github.com:443 via XXXXXXXXX** 的文字，反复尝试，将这些网址加入pac规则即可。