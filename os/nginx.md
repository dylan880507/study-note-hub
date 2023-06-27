## 1>相关文章

###### [Nginx配置-启用gzip压缩，优化网站访问速度](https://blog.csdn.net/chenthe1/article/details/123896204)

## 2>常用命令

###### `start nginx` (启动)

###### `nginx -s stop` (快速停止nginx)

###### `nginx -s quit` (完整有序的停止nginx)

###### `nginx -s reload` (修改配置文件后使用)

###### `nginx -t` (测试配置文件是否正确)

###### `tasklist /fi "imagename eq nginx.exe"` (查看nginx是否启动成功)

###### `taskkill /f /t /im nginx.exe` (强制停止服务)

###### `nginx -V` (查看nginx配置的模块)

###### `netstat -ano` => 查看当前本机的所有端口情况

###### `netstat -aon|findstr 端口号` => netstat -aon|findstr 9002, 查看使用9002端口的进程

###### `tasklist|findstr 进程ID` => tasklist|findstr 4, 查看进程id对对应的应用
