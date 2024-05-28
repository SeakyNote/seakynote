## 发行版

### Arch Linux

- 这是一个白手起家的发行版
- 比较适合于 DIY
- 默认装出来的系统近乎全裸，然后根据你的需要，安装自己喜欢的软件包
- 它的设计理念是KISS 原则，追求简洁主义。定位于有技术背景的熟练用户

### Ubuntu

- 影响力最大的桌面发行版
- 美中不足之处是——Ubuntu 本身是一家【商业】公司维护的

### Linux Mint

- 衍生自 Ubuntu Desktop
- 由社区维护
- 很强调【傻瓜化】的用户体验，所以吸引到不少人气。

### Manjaro Linux

- 侧重于降低 Arch 的使用门槛
- 也由商业公司维护

## issues

### 常规

#### 缩放

- gnome——仅整数倍，workaround `sudo pacman -S mutter-x11-scaling gnome-control-center-x11-scaling`
- kde——自带缩放；缩放1.5倍右侧可能有白边，调整成1.25/1.6倍
- xfce——https://seekstar.github.io/2023/02/23/xfce%E9%AB%98%E5%88%86%E5%B1%8F%E7%BC%A9%E6%94%BE/

#### 输入法

https://www.jianshu.com/p/1b3def9435b6

错误: 无法读取数据库 'extra' (Damaged tar archive)——源不对

在X11上会有吞字现象，在Wayland上则没有

#### 如何禁止自动回到欢迎界面

搜索锁屏

#### 程序标题栏恢复

alt+F3

#### 软件删除

- 一般——包管理器
- 第三方——删除文件、文件夹

#### tar.gz

对应压缩包

#### pkg.tar.zst

对应安装包

#### 安装snap

https://snapcraft.io/docs/installing-snapd

https://snapcraft.io/docs/installing-snap-store-app

#### faltpak换源

`sudo flatpak remote-modify flathub --url=https://mirror.sjtu.edu.cn/flathub`

#### 安装deb文件

debtap

#### 导入证书

转pem——https://blog.csdn.net/swallowcosmos/article/details/103353721

#### 找到某软件的配置文件

`locate kchmviewer`

### 家用软件

snipaste——Spectacle截图工具

xmind——OK

everything——catfish，默认搜索

qBitorrent——OK

honeyViewer——gwenviewer

chm——kchmviewer

calibre——OK

foobar2000——elisa音乐播放器

localsend——OK

typora——github上下载0.11.18

splashtop——NOK

notepad++——notapadqq

sumatrapdf——okular

tortoiseGit——gitg，Kommit

obs——OK

vscode——官网下载deb，flatpak版隔离了本机环境

chrome——chromium

logitech G Hub——NOK

7z——Ark压缩文件管理工具

potplayer——vlc

### 工作软件

citrix——`pamac build icaclient`

citrix导入证书——https://blog.csdn.net/gikod/article/details/105164682

cmake——OK

qt5/6——操作跟windows安装成套的不太一样，如何改版本待研究

飞书——OK

微信——NOK

### 物理机

uefi引导——安装时虚拟机使用uefi模式

安装虚拟机

- vmware安装流程——https://www.jianshu.com/p/a0ccf792d425
- ncurses5-compat-libs安装问题——https://forum.manjaro.org/t/i-cant-intall-ncurses5-compat-libs/138054
- manjaro本身不在vmware的支持清单中，疑似引发系统不稳定，优先使用virtualbox

显示器亮度控制

- 多显示器联动调整——系统设置，亮度
- 单独调整——ddcutil

cpu/内存状态——kde挂件

硬盘测速——KDiskMark