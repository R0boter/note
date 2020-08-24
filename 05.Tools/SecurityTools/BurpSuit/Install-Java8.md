## Linux

1. 从github下载JAVA8

2. 将下载下来的包解压到`/usr/share/java/`

3. 设置环境变量
   
   ```shell
   vim ~/.bashrc
   # set java environment
   export JAVA_HOME=/usr/share/java/jdk1.8.0_212
   export JRE_HOME=${JAVA_HOME}/jre
   export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
   export PATH=${JAVA_HOME}/bin:$PATH
   ```

4. 一定要将环境变量设置为全部用户,写入到`/etc/profile`文件,否则Burpsuite的快捷方式点击无反应,且jd-gui不显示图标
