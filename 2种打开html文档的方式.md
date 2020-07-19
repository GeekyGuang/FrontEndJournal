# 2种打开html文档的方式

### 1. http-server
安装：`yarn global add http-server`
运行：`http-server . -c-1` 或者 `http-server -c-1`  // -c-1代表不要缓存
http-server可简写为hs：`hs -c-1`
如果浏览器输入地址后无法显示，在地址后加上文件名
http://127.0.0.1:8080/index.html


### 2. parcel
安装：`yarn global add parcel`
运行：`parcel index.html`




