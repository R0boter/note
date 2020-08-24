### Windows下配置CURL文件

进入Git安装目录下的cmd文件夹，新建文本，将下列代码放入文本后，将文件名改为curl.cmd

```git
@rem Do not use "echo off" to not affect any child calls.
@setlocal

@rem Get the abolute path to the parent directory, which is assumed to be the
@rem Git installation root.
@for /F "delims=" %%I in ("%~dp0..") do @set git_install_root=%%~fI
@set PATH=%git_install_root%\bin;%git_install_root%\mingw\bin;%git_install_root%\mingw64\bin;%PATH%
@rem !!!!!!! For 64bit msysgit, replace 'mingw' above with 'mingw64' !!!!!!!

@if not exist "%HOME%" @set HOME=%HOMEDRIVE%%HOMEPATH%
@if not exist "%HOME%" @set HOME=%USERPROFILE%

@curl.exe %*
```
