# 快速入门

## 启动一个nginx服务

```shell
docker run -p 8000:80 --name ngx_demo -d nginx
```
```bash
#
# 参数说明
#    -p 
#       8000:80 表示将 docker container 的80端口映射的主  机的8000 端口 
#    --name 
#       表示给这个container 取个名字 
#    -d 
#       表示让container 运行在后台，不然这个会占据你的命令行窗口
```

<div align=left><img src="_images/docker/docker-quickstart-nginx.gif#pic_center" height="382" width="618"></div>

## 启动一个mysql服务

```shell
docker run --name some-mysql -p 3306:3306 -v /my/own/datadir:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql:8.0.21
```
```shell
# 参数说明
#   -v <主机目录>:<容器里的目录>   将容器的数据持久化
```

```shell
mysql -h 127.0.0.1 -u root -p123456    #默认访问主机的3306端口
```
<div align=left><img src="_images/docker/docker-quickstart-mysql.gif#pic_center" height="382" width="618"></div>

