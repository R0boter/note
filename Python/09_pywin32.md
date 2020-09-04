# pywin32 模块

## 前言

1. pywin32是python中的第三方库，需下载安装后才能使用其中的模块
2. 在shell中使用`python -m pip install pywin32`安装，或去官网下载安装
3. pywin32库中的模块都是用于windows编程的，相当于将windowsAPI封装成python可直接调用
4. 要获取窗口类名和标题等，可以使用spyLite或spy++

## win32con

## win32gui

win32gui库是对窗体的控制

```python
win_name = win32gui.FindWindow("类","标题")    # 找到窗口，将它赋值给一个变量名
win32gui.ShowWindow(win_name,win32con.SW_HIDE)    # 隐藏窗口
win32gui.ShowWindow(win_name,win32con.SW_SHOW)    # 显示窗口

# 控制窗口位置，参数1:窗体名,参数2:大致方位,win32con.HWND_TOPMOST表示上方，x和y是指定x轴和y轴的位置，width_size和height_size是指定窗体的宽和高,win32con.SWP_SHOWWINDOW表示窗体保持显示
win32gui.SetWindowPos(win_name,win32con.HWND_TOPMOST,x,y,width_size,high_size,win32con.SWP_SHOWWINDOW)
```

### win32com

1. `win32com.client`：系统客户端

   ```python
   import win32com.client
     # 返回一个可以使用语音的对象
     speaker = win32com.client.Dispatch("SAPI.SPVOICE")
     # 调用这个对象将string以语音方式输出,
     speaker.Speak("string")
     # Tips:要使程序能输出语音，需在系统中先打开语音识别
   ```
