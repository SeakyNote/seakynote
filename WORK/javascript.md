## npm切换源

### 切换源

`npm config set registry https://registry.npm.taobao.org`

`npm config set registry https://mirrors.huaweicloud.com/repository/npm/`

### electron切换源

`set ELECTRON_MIRROR=http://npm.taobao.org/mirrors/electron/`

`set ELECTRON_MIRROR=https://mirrors.huaweicloud.com/electron/`

要用华为源，淘宝源少东西

### 若换源仍无法下载某些文件

如winCodeSign

则将该文件解压缩拷到缓存目录下

AppData/Local/electron-builder/Cache

### 解决electron-builder打包时下载依赖慢的问题

https://www.azimiao.com/6208.html

## Vue 报错error:0308010C:digital envelope routines::unsupported

https://blog.csdn.net/zjjxxh/article/details/127173968