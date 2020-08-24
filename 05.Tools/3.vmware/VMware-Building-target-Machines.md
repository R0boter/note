### 	NAT模式下VMware网络编辑器设置

直接将虚拟机设置为NAT模式也可以访问外网，这个笔记是为了实现宿主机和虚拟机互相PING通，并且能远程桌面连接虚拟机 

下图是VMware虚拟网络编辑器的截图：
![NetWorkEdit](https://i.loli.net/2019/01/11/5c38bceece743.png "虚拟网络编辑器")  
首先在VMware的编辑选项打开虚拟网络编辑器，然后点击右下角的更改设置。  

1. 首先选择VMnet8(关于VMnet在VMware三种网络模式笔记中有讲)

2. 子网IP设置如图，这个是根据掩码来设置的ip范围起始地址
   
   > 例：子网掩码为255.255.255.0 那么子网ip范围192.168.1.0~192.168.1.255，起始地址就是192.168.1.0   

3. 设置子网掩码(ip知识在网络基础知识笔记本)

4. NAT设置，这里是不能设置为VMnet8的IP，这个其实是一个虚拟网关  
    ![NATSet](https://i.loli.net/2019/01/11/5c38bceecba52.png "NAT设置")    
   
   > 这里的IP设置在刚刚设置的IP范围内就行  
   
   ### 设置虚拟机

5. 首先需要将虚拟机的IP配置为静态IP
   
   > IP刚刚设置的子网IP范围内
   > 
   > 子网掩码跟上面设置的一样
   > 
   > 网关为NAT设置中设置的网关IP
   > 
   > DNS设置为网关的IP(其实无所谓，设置114或不设置都行，保险起见设置为网关IP) 

6. 检查支持共享功能的服务是否启动，Win+R输入services.msc然后在右边查找以下的三个服务
   
   > Function Discovery Resource Publication  
   > 
   > SSDP Discovery  
   > 
   > UPnP Device Host  
   > 
   > 如果没有开启就将他们开启，如果显示禁用，右键选择属性，选择自动或手动，然后就可以启动了(最好将他们属性设置为自动)  

7. 开启网络发现，在控制面板 -> 网络和共享中心 -> 左边有更改高级共享设置，这里就可以启用网络发现 
   
   Tips：注意自己的网络类型是公用还是专用还是什么，要在对应的网络类型里启用网络发现  

8. 启用远程连接，在我的电脑的属性里面有远程设置，在远程桌面那一栏将允许远程桌面连接到此计算机勾上就行  

9. 给你的账户设置密码，因为远程连接默认不允许空密码连接，所以需要给你的账户设置一个密码

### 设置宿主机

1. 控制面板里的网络和共享中心，左边选择更改适配器选项，将VMware Network Adapter VMnet8的地址改为上面设置的网关地址
2. 开启网络发现
3. 测试虚拟机和宿主机能不能互相PING通，能的话就说明成功了，然后就可以使用远程桌面连接虚拟机了

### 关于系统不同的几个坑

1. Windows2003设置用户密码在我的电脑右键管理里面的组和用户里，选择要设置密码的账户，右键才有设置密码
2. Windows2012和2016要打开计算机管理需要在服务器管理的右上角的工具选项里打开

### Debian搭建靶机

1. 最小化安装后设置静态IP和DNS地址  
   
   ```Linux
   vim /etc/network/interfaces        #修改网卡配置文件，添加下面的内容
   auto interfacesname
   iface interfacesname inet static    #static表示静态，dhcp表示动态分配
   address xxx.xxx.xxx.xxx            #分配的IP地址
   netmask xxx.xxx.xxx.xxx            #子网掩码
   gateway xxx.xxx.xxx.xxx            #网关IP地址
   
   vim /etc/resolv.conf                #修改DNS地址
   nameserver xxx.xxx.xxx.xxx            #将这个选项改为需要设置的DNS即可，也可以再设置一个备用的DNS
   
   service networking restart            #重启网络服务
   ```

2. 修改更新源`vim /etc/apt/sources.list`#更新并安装SSH  

3. 设置SSH服务允许root用户登录  
   
   ```bash
   vim /etc/ssh/sshd_config            #修改SSH服务配置文件  
   PermitRootLogin prohibit-password    #将这条语句改为PermitRootLogin yes(去掉前面的注释)  
   service ssh restart                #重启SSH服务  
   ```
