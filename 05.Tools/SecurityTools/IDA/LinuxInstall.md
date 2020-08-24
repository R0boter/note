## 启用32位环境

`dpkg --add-architecture`

`apt-get update`

## 安装依赖

`apt-get install libc6-i686:i386 libexpat1:i386 libffi6:i386 libfontconfig1:i386 libfreetype6:i386 libgcc1:i386 libglib2.0-0:i386 libice6:i386 libpcre3:i386 libsm6:i386 libstdc++6:i386 libuuid1:i386 libx11-6:i386 libxau6:i386 libxcb1:i386 libxdmcp6:i386 libxext6:i386 libxrender1:i386 zlib1g:i386 libx11-xcb1:i386 libdbus-1-3:i386 libxi6:i386 libsm6:i386 libcurl3:i386`

## 设置快捷图标

将文件夹中的两个`desktop`结尾的文件移动到`/usr/share/applications/`文件夹下

`desktop`文件写法如下：

```ini
[Desktop Entry]
Name=xxx
Exce=/path/to/executable/file
Icon=/path/to/executable/file/icon or png
Type=Application
Terminal=false
Comment=xxx xxx
```

