## 安装

`sudo apt-get install wireshark`

Tips：普通用户启动会报没有权限，解决方法是添加一个wireshark组，并将当前用户加入到这个组

```shell
sudo groupadd wireshark
sudo chgrp wireshark /usr/bin/dumpcap
sudo chmod 4755 /usr/bin/dumcap
sudo gpasswd -a UserName wireshark
```
