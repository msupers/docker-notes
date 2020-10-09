# Dockerfile命令详解
?>文件指令集，用来说明如何创建Docker镜像

- dockerfile指令忽略大小写，建议大写，`#`作为注释，每行只支持一条指令，指令可以带多个参数。

- dockerfile指令分为`构建指令`和`设置指令`。

一个示例：

```shell
FROM ubuntu:18.04
MAINTAINER Tom
USER root
ENV JAVA_HOME /opt/java/jdk1.8.0_91
RUN apt-get update
RUN apt-get install -y nginx
ADD ./go1.11.linux-amd64.tar.gz /usr/local/
COPY ./go1.10.linux-amd64.tar.gz /usr/local/go/
WORKDIR /opt
ENTRYPOINT ["nginx"]
CMD ["-g","daemon off;"]

```

## 构建指令

?>`构建指令`：用于构建image，其指定的操作`不会`在运行image的容器中执行。

### FROM
?>指定基础镜像<br/>在基础镜像的基础上修改数据从而构建新的镜像。基础镜像可以是本地仓库也可以是远程仓库。

指令有两种格式：

- FROM image 【默认为latest版本】
- FROM image:tag 【指定版本】

```shell
FROM ubuntu:18.04
```

### MAINTAINER
?>镜像创建者信息<br/>将镜像制作者（维护者）的信息写入image中，执行docker inspect时会输出该信息。

```shell
MAINTAINER zhangmiao334@xdf.cn
```

### ADD
?>从src复制文件到container的dest路径<br/>复制指定的src到容器中的dest，其中src是相对被构建的源目录的相对路径，可以是文件或目录的路径，也可以是一个远程的文件url，dest 是container中的绝对路径。<br/>所有拷贝到container中的文件和文件夹权限为0755，uid和gid为0。

- 如果src是一个目录，那么会将该目录下的所有文件添加到container中，`不包括目录`
- 如果src文件是可识别的压缩格式(tar.gz)，则docker会帮忙解压缩（注意压缩格式）；
- 如果src是文件且dest中不使用斜杠结束，则会将dest视为文件，src的内容会写入dest；
- 如果src是文件且dest中使用斜杠结束，则会src文件拷贝到dest目录下。

```shell
ADD ./abc.tar.gz /usr/local/
```

### RUN

?>在制作镜像的`临时`容器中运行命令<br/>RUN可以`运行`任何被基础镜像支持的`命令`（即在基础镜像上执行一个进程），可以使用多条RUN指令，指令较长可以使用`\`来换行。

指令有两种格式：

- RUN <linux command> (the command is run in a shell - /bin/sh -c)
- RUN [“executable”, “param1”, “param2” … ] (exec form)

```shell
RUN yum install wget -y
```
```shell
RUN["/bin/bash","-c",“echo hello”]
```


### ENV
?>在image中设置环境变量`以键值对的形式`，设置之后RUN命令可以使用该环境变量.<br/>在容器启动后也可以通过docker inspect查看环境变量.<br/>通过 docker run --env key=value在容器启动时设置或修改环境变量。

```shell
ENV JAVA_HOME /path/to/java/dirent
```

## 设置指令 

?>`设置指令`：用于设置image的属性，其指定的操作`会`在运行image的容器中执行。

### CMD

!>用于容器启动时的指定操作，可以是自定义脚本或命令，只执行一次，多个默认`执行最后一个`。

指令有三种格式：

- CMD [“executable”,“param1”,“param2”] (like an exec, this is the preferred form)

- CMD command param1 param2 (as a shell)

- CMD [“param1”,“param2”] (as default parameters to ENTRYPOINT)

```shell
["catalina.sh", "run"]
```

```shell
["java","-jar","-Dspring.profiles.active=pre","/neworiental/project/application/qm-center-service/qm-center-service-0.0.1-SNAPSHOT.jar"]
```

### ENTRYPOINT

?>设置container启动时执行的操作<br/>

- 指定容器启动时执行的命令，若多次设置只执行最后一次。
- ENTRYPOINT翻译为“进入点”，它的功能可以让容器表现得像一个可执行程序一样。

### USER

?>设置启动容器的用户，默认为root用户。

```shell
USER <linux user>
```

### EXPOSE

?>指定容器需要映射到宿主机的端口

- 该指令会将容器中的端口映射为宿主机中的端口`确保宿主机的端口号没有被使用`。
- 通过宿主机IP和映射后的端口即可访问容器`避免每次运行容器时IP随机生成不固定的问题`。
- 前提是EXPOSE设置映射端口，运行容器时加上-p参数指定EXPOSE设置的端口。
- EXPOSE可以设置多个端口号，相应地运行容器配套多次使用-p参数。
- 可以通过docker port +容器需要映射的端口号和容器ID来参考宿主机的映射端口。

```shell
EXPOSE port [port…]
```

