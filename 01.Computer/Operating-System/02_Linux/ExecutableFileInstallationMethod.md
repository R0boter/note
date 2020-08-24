## Bundle

先用chmod +x 添加可执行权限，然后直接运行就可以了

## Ded

使用dpkg -i 执行安装

使用dpkg -e 执行卸载

使用dpkg -l 查看当前系统中已安装软件，可以加软件名以查看在源文件里是否有这个软件

## gar.gz源代码

这是打包好的源码，需要自己编译安装。

首先解压缩：`tar -zxvf 包名`  

然后切进解压缩后的文件夹里，执行`./configure`为编译做准备  

编译`make`，安装`make install`，清理`make (dist)clean`

## tar.gz2源代码

跟gar.gz一样的安装方法，只是解压缩需要用`tar -jxvf`，因为两种包是用不同的工具打包的所以需要不同的命令解压

## 通过debian系自带的apt-get命令安装

``apt-cache search 'soft'``soft是指你要安装的软件名或相关信息，这句话是在包列表中搜索对应的包名，查看是否有这个软件，以及软件的版本号

找到后使用:``apt-get install 'soft'``命令直接安装即可，如果没找到，建议换源或更新源列表，如果确实没有就去github或该软件官网下载然后安装

## 不需要安装的压缩包

解压缩后，使用chmod命令添加可执行权限后直接运行其中的软件，可以将该文件夹移动到一个用户安装软件的文件夹中，然后使用`ln -s softwarename /bin/`在bin目录下建立一个指向该软件的链接，这样就可以在任意路径启动该软件，在/usr/share/applications目录可以建立桌面图标
