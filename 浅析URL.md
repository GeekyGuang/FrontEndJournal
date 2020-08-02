# 浅析URL

### 几个名词
HTTP(HyperText Transfer Protocol, 超文本传输协议)
IP(Internet Protocol, 网际互连协议)
URL(Uniform Resource Locator, 统一资源定位器)
DNS(Domain Name System, 域名系统)


### IP
作用： 用于定位一台设备


IP分为内网IP和外网IP
路由器即网关，同时有内网IP和外网IP


几个特殊IP:

- 127.0.0.1表示自己
- localhost通过hosts指定自己
- 0.0.0.0不表示任何设备



`ping baidu.com`  // 查看IP


### 端口 port
作用：用来定位设备上的不同服务


0-1023端口只留给系统用
普通用户用其他端口
http服务默认是端口80
https服务默认是端口443


`http-server -c-1 -p 1234`  // 指定端口


IP定位设备，端口定位服务，IP和端口缺一不可


### 域名 Domain Name
作用：域名是对IP的别称


一个域名可以对应多个不同IP, 负载均衡
一个IP也可以对应多个域名，共享主机


com是顶级域名
baidu.com中的baidu是二级域名(俗称一级域名)
xxx.github.io中的xxx是三级域名(俗称二级域名)


aaa.com和www.aaa.com可以不是同一家公司

### DNS
作用：将域名和IP相互映射


`nslookup baidu.com`  // 通过域名查看IP


### URL
URL = 协议 + 域名或IP + (端口号) + 路径 + 查询字符串 + 锚点
https://www.baidu.com/s?wd=hello&rsv_spt=1#5


- 路径：用于请求不同页面
- 查询参数：用于请求同一页面不同内容
- 锚点：用于请求同一内容不同位置
   - 锚点不支持中文
   - 锚点不会传给服务器



### curl命令
作用：发HTTP请求，支持上传和下载


`curl -v http://baidu.com`
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1595778069145-5c2dabc1-7833-4391-80a2-e81bcc5276ed.png#align=left&display=inline&height=322&margin=%5Bobject%20Object%5D&name=image.png&originHeight=375&originWidth=714&size=36966&status=done&style=none&width=613)
发生了什么？

- url被curl工具重写，请求DNS获取IP
- 进行TCP连接，连接成功后发HTTP请求
- 请求内容看一眼
- 响应内容看一眼
- 响应结束后关闭TCP连接
- 真正结束



