**它的创始人是 Linus**

**Git 的成功应用案例，俺不说大伙儿应该猜得到是：Linux Kernel。光这一个就足够说明问题了。**

## 托管服务

公开：github，2019/1开始可以建私有仓库

私有：bitbucket

## SourceTree

**跨平台**

安装问题：此操作系统不支持 .NET Framework 4.8.1

下载离线版：

https://download.visualstudio.microsoft.com/download/pr/2d6bb6b2-226a-4baa-bdec-798822606ff1/8494001c276a4b96804cde7829c04d7f/ndp48-x86-x64-allos-enu.exe

## 提交

为什么一定有提交注释——记录"为什么进行了变更"

## fork

河流或道路的分支

## 拉取请求

pull request——请求对方拉取你的代码

## Git - SSL_ERROR_SYSCALL

https://blog.csdn.net/Kanmeijie/article/details/120745367

Edit global .gitconfig

[http]
        proxy = socks5://127.0.0.1:7891
[https]
        proxy = socks5://127.0.0.1:7891

7891为对应clash设置的端口号

## gitignore模板

https://github.com/github/gitignore

## revert

回滚提交——新增一次提交，将之前的提交取消

## rebase

提交历史合并成一条直线

re+base——把分支连根拔起，重新栽种

## squash

合并多个提交

## 拉取pull

pull=fetch+merge

## fetch

只更新远程跟踪分支

本地分支未更新

------

在detached HEAD状态下提交后，可通过创建新分支解决

## git的好处

回到历史状态

信息透明——变更历史+变更原因都有记录

方便交流