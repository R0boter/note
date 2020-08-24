## 简介

Nginx是一个HTTP服务器、反向代理服务器、邮件代理服务器、通用TCP/UDP代理服务器。由俄国人Igor Sysoev(伊戈尔-西索夫)编写

## 配置文件路径、结构

1. 路径

   如果是编译安装，则配置文件路径由`--conf-path`指定，若未使用此参数指定则配置文件路径在`--prefix`指定的路径下的`config/`文件夹下，若未指定安装路径，则配置文件在默认路径下，Debian下的`/etc/nginx`

   如果忘记配置文件位置可以使用`sudo nginx -V`查看编译时的配置参数。或者使用`sudo nginx -t`命令，此命令用于检查nginx配置文件是否有语法错误，如果没有就会显示出配置文件路径，并提示`syntax is ok,test is successful`

2. 结构

   ```shell
   tree /etc/nginx
   /etc/nginx/
   ├── conf.d
   ├── fastcgi.conf
   ├── fastcgi_params
   ├── koi-utf
   ├── koi-win
   ├── mime.types
   ├── modules-available
   ├── modules-enabled
   │   ├── 50-mod-http-auth-pam.conf -> /usr/share/nginx/modules-available/mod-http-auth-pam.conf
   │   ├── 50-mod-http-dav-ext.conf -> /usr/share/nginx/modules-available/mod-http-dav-ext.conf
   │   ├── 50-mod-http-echo.conf -> /usr/share/nginx/modules-available/mod-http-echo.conf
   │   ├── 50-mod-http-geoip.conf -> /usr/share/nginx/modules-available/mod-http-geoip.conf
   │   ├── 50-mod-http-image-filter.conf -> /usr/share/nginx/modules-available/mod-http-image-filter.conf
   │   ├── 50-mod-http-subs-filter.conf -> /usr/share/nginx/modules-available/mod-http-subs-filter.conf
   │   ├── 50-mod-http-upstream-fair.conf -> /usr/share/nginx/modules-available/mod-http-upstream-fair.conf
   |   ├── 50-mod-http-xslt-filter.conf -> /usr/share/nginx/modules-available/mod-http-xslt-filter.conf
   │   ├── 50-mod-mail.conf -> /usr/share/nginx/modules-available/mod-mail.conf
   │   └── 50-mod-stream.conf -> /usr/share/nginx/modules-available/mod-stream.conf
   ├── nginx.conf
   ├── proxy_params
   ├── scgi_params
   ├── sites-available
   │   └── default
   ├── sites-enabled
   │   └── default -> /etc/nginx/sites-available/default
   ├── snippets
   │   ├── fastcgi-php.conf
   │   └── snakeoil.conf
   ├── uwsgi_params
   └── win-utf
   ```

## 配置文件解释

1. **nginx.conf**：nginx主配置文件，nginx只承认此配置文件，其他配置文件如果用到需要在**nginx.conf**里用`include`指令包含进来

2. **conf.d**：用户自定义配置文件目录，用于存放用户在不改动主配置文件时自己写的配置配置文件。可以在**nginx.conf**用`includ conf.d/*`将此文件夹下所有配置文件全部包含进来也可以指定包含单个自定义配置文件

3. **fastcgi_params**：指定**fastcgi**参数。比如php-fpm就是一个fastcgi。当你在nginx中使用`fastcgi_pass`把`.php`的文件交给php-fpm处理时，就需要把fastcgi_params参数传递过去。PHP中的`$_SERVER`超全局数组中的各种元素正是来自fastcgi_params中定义的变量

   格式：`fastcgi_param 参数名 参数值`

   其中参数值是nginx内置变量，nginx有很多内置变量，具体去[nginx官网的http模块]( https://nginx.org/en/docs/http/ngx_http_core_module.html )的`Embadded Variables`目录中查看

   > 例子：在**fastcgi_params**中定义了`fastcgi_param REMOTE_ADDR $remote_addr;`。而[PHP中的超全局数组]( https://www.php.net/manual/zh/language.variables.superglobals.php )`$_SERVER`中用于获取客户端IP的变量`$_SERVER['REMOTE_ADDR']`正是来自上面的定义
   
4. **fastcgi.conf**：与**fastcgi_param**文件几乎一样，是nginx不同发展阶段的产物，最开始使用fastcgi_param，后面添加的fastcgi.conf。其中最主要的区别就是fastcgi.conf中增加了一句`fastcgi_param  SCRIPT_FILENAME    $document_root$fastcgi_script_name;`。原因是以前的nginx中是没有`$document_root`这个变量，需要写死document_root路径，后面nginx添加了此变量后，照顾用户习惯，就新建立了fastcgi配置文件用新的写法，而老配置文件保持以前的习惯，这样防止重复定义。推荐使用新配置`include fastcgi.conf`

5. **scgi_param**和**uwsgi_param**：和fastcgi_param是同一类型文件，但PHP只会用到fastcgi所以这两个文件一般不用

6. **koi-utf**和**koi-win**：用于支持俄语等斯拉夫语系语言的编码及映射文件(nginx是俄罗斯人编写)

7. **win-utf**：用于解决windows乱码问题的编码映射文件

8. **mime.types**：定义nginx支持的mime文件格式，主要用于定义不同扩展名对应的mime类型

   ```nginx
   type {
   #   mime类型							 对应的文件扩展名
       text/html                             html htm shtml;
       text/css                              css;
       text/xml                              xml;
       image/gif                             gif;
       image/jpeg                            jpeg jpg;
       application/javascript                js;
       application/atom+xml                  atom;
       application/rss+xml                   rss;
   }
   ```

9. **proxy_params**：代理参数相关，Debian下默认内容如下

   ```nginx
   proxy_set_header Host $http_host;
   proxy_set_header X-Real-IP $remote_addr;
   proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
   proxy_set_header X-Forwarded-Proto $scheme;
   ```

10. **modules-available**和**modules-enabled**：用于启用nginx其他的非默认模块，具体方法是在**modules-available**中创建启用nginx其他模块的配置文件一般为`load_module modules_path`。然后在**modules-enabled**中创建**modules-available**下配置文件的链接文件。这样就启用了nginx中的相应功能的模块

11. **sites-available**和**sites-enabled**：用于用户自定义的虚拟主机(网站)的配置文件(即nginx配置i文件中的server块，可以通过`include`指令包含进配置，方便批量配置)，有些写作**vhost**。具体方法参考上面nginx模块功能配置文件的使用方法

## HTTP服务器

HTTP服务器的具体配置在nginx配置文件中的HTTP块中定义

一个HTTP服务器可以包含多个虚拟主机(virtual host)，一个网站为一个虚拟主机

## 虚拟主机

虚拟主机的配置在nginx中的server块中

一个网站为一台主机，通过在一台服务器上搭建多个网站，实际上是这一台服务器虚拟成多个主机，各自互不影响，所以称一个网站为一台虚拟主机





​      

​      

​      

​      

​      





