## 前言

nginx的各个功能是由对应的模块提供的，每个模块在配置文件中都有对应的块。

其中nginx自带的功能分别是主模块和事件模块

主模块对应的是配置文件中的全局块，事件模块对应的是配置文件中的事件管理块

而HTTP块实际是由HTTP Core Moudle提供的，还有的一些nginx中的基本模块如下

## HTTP Upstream Moudle

upstream块包含在http块中，可以包含多个，用于将多个用于轮询的后端服务器绑定到一个upstream_name中，在location块中使用`proxy_pass	http://upstream_name`进行调用

```nginx
http {
    upstream backend {
        # 设置使客户端的请求总是连接到同一个后端服务器或IP，以减少轮询次数，提高效率，当请求的后端服务器无效时会自动转接其他服务器
        ip_hash;
        
        # 设置后端参与轮询的服务器IP或虚拟主机名
        server backend1.example.com weight=5;
        server backend2.example.com:8080;
        server unix:/tmp/backend3;
        server 192.168.1.1;
    }
    
    server {
        location / {
            proxy_pass http://backend;
        }
    }
}
```



## HTTP Access Moudle



## HTTP Auth Basic Moudle



## HTTP AutoIndex Module



## Browser



## Charset



## Empty GIF



## FastCGI



## Geo



## Gzip



## HTTP Headers Moudle



## HTTP Index Module



## HTTP Referer Moudle



## HTTP Limit Zone Moudle



## HTTP Limit Requests Moudle



## Log



## Map



## Memcached



## HTTP Proxy Moudle



## Rewrite



## SSI Moudle



## User ID