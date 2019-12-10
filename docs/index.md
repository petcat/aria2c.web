# 首页

Welcome! 这是一个介绍使用 Aria2 用来搭建个人网盘的网站，如果你需要个人网盘，你这是来对了。首先，你需要一只“大盘鸡” -- [大硬盘VPS](https://aria2c.cn/vps/)，如果你还没有，请先购买，有关[大硬盘储存型 VPS Hosting](https://aria2c.cn/vps/)，请阅读：[https://aria2c.cn/vps/](https://aria2c.cn/vps/)  
本站使用开源[mkdocs](https://github.com/mkdocs/mkdocs/) build.

## aria2

Aria2 是一款自由、跨平台命令行界面的下载管理器，支持的下载 HTTP、HTTPS、FTP、Bittorrent和Metalink 协议格式的文件，也就是支持普通的网页下载和BT下载（也支持PT）。有关 Aria2 的介绍请阅读：[https://aria2c.cn/about/](https://aria2c.cn/about/) 

### aria2 安装

debian 系，包括 ubuntu ，直接 `apt install aria2` 即可安装，强烈建议使用 debian 系，不得不吐槽一下，国内习惯完全是歪的，新手完全不建议使用 CentOS ，我都不敢使用 CentOS ，无它，难用就一个字。万年不更的老库所谓的”稳定“，所有软件都是老掉牙，想用个软件都要编译，可能会有人反驳，你可以用第三方库啊。我说，你既然敢接受第三方库的，那你为什么不干脆直接使用 debian 的官方库？

如果你需要编译安装 aria2 最新版本，请阅读：[https://aria2c.cn/about/](https://aria2c.cn/about/)    

### aria2 使用

aria2c 典型命令行使用例子：

```
# HTTP下载
aria2c http://example.org/mylinux.iso
# 磁力链下载
aria2c 'magnet:?xt=urn:btih:248D0A1CD08284299DE78D5C1ED359BB46717D8C'
```

当然，这里不是，因为 aria2 支持 RPC 远程下载，这才是 aria2 的最大的优点

#### 1、简单篇：

安装后执行命令：`aria2c --enable-rpc --rpc-listen-all=true --rpc-allow-origin-all --rpc-secret=aria2c.cn --dir=/home -D`  

这条命令的意思就是打开 aria2 的 RPC 下载，并设置下载密钥为 `aria2c.cn` 下载目录为 `/home` 

下载目录和下载密钥，可自行修改设置。

##### AriaNG 

AriaNG 是一个 aria2 的 Web 前端，官网：[https://github.com/mayswind/AriaNg](https://github.com/mayswind/AriaNg)

你可以通过 Chrome 商店的浏览器扩展：[Aria2 for Chrome](https://chrome.google.com/webstore/detail/aria2-for-chrome/mpkodccbngfoacfalldjimigbofkhgjn)  或直接打开 [http://ariang.xyz](http://ariang.xyz)  使用 AriaNG 调用 RPC 实现远程下载。

左侧菜单，AriaNG 设置 ---- 新填一个，然后填上你的IP和密钥，刷新后即可开始你的下载

#### 2、进阶篇

……

## filebrowser

[filebrowser](https://github.com/filebrowser/filebrowser/) 是一个Go语言写的文件浏览器，简洁干净，提供文件的浏览，目前支持文本文件在线浏览和修改，图片文件、mp4 视频文件在线播放，及文件的上传、下载、移动、复制、重命名、删除等操作，并且支持Linux SSH 命令，比如git 、zip等等命令，具有多用户、不同用户分配不同权限的功能，实在是居家必备的优秀软件。   

### 安装 filebrowser

官方命令： `curl -fsSL https://filebrowser.xyz/get.sh | bash`   

### 配置

创建配置数据库：`filebrowser -d /etc/filebrowser.db config init`  

设置监听地址：`filebrowser -d /etc/filebrowser.db config set --address 0.0.0.0`   

设置监听端口：`filebrowser -d /etc/filebrowser.db config set --port 8088`   

设置语言环境：`filebrowser -d /etc/filebrowser.db config set --locale zh-cn`   

设置日志位置：`filebrowser -d /etc/filebrowser.db config set --log /var/log/filebrowser.log`    

添加 Admin 用户和密码（其中的root和password分别是用户名和密码，根据自己的需求更改）：`filebrowser -d /etc/filebrowser.db users add root password --perm.admin`    

设置完成后，然后命令 `setsid /usr/local/bin/filebrowser -d /etc/filebrowser.db &`   让 filebrowser 在后台一直运行。

### 开机启动 (/etc/rc.local):

现在 filebrowser 已经可以正常使用了，为了重启也能自动运行，我们需要编辑 rc.local 支持开机启动, 命令：`nano /etc/rc.local`  在最后 exit 0 前添加上 `setsid /usr/local/bin/filebrowser -d /etc/filebrowser.db &`      



### 使用

现在你已经可以打开 http://123.123.123.123:8088 （换成自己的IP）使用你设置的用户名和密码，登录管理你的下载的文件了。mp4 文件直接可以在线播放。
