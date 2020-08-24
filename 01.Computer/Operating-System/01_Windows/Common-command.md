# Windows 常用命令

## 计划任务

AT命令已经在新版windows下被废除，应当使用`schtasks`。

但简体中文的schtasks MUI语言包有问题导致`schtasks /query`命令无法输出(显示：无法加载列资源)。`schrtasks`默认动作就是`schtasks /query`，但其他命令是正常的。可以使用命令`chcp 437`将字符集设置为英文，就可以使用该命令

```CMD
    /Create         创建新计划任务。
    /Delete         删除计划任务。
    /Query          显示所有计划任务。
    /Change         更改计划任务属性。
    /Run            按需运行计划任务。
    /End            中止当前正在运行的计划任务。
    /ShowSid        显示与计划的任务名称相应的安全标识符。
    /?              显示此帮助消息。
```
