# 核心概念

?>Docker不是虚拟机。<br/>Docker本质是宿主机上的进程。<br/>docker通过`namespace`实现`资源隔离`，通过`cgroup`实现`资源限制`。<br/>通过写时拷贝机制(`copy on write`)实现高效的文件操作。

## Docker架构

?>docker是一个C/S模式的架构，后端是一个松耦合架构，模块各司其职。

<div align=left><img src="_images/docker/docker-architecture.jpg#pic_center" height="618" width="582"></div>

- 用户是使用`Docker Client`与Docker Daemon建立通信，并发送请求给后者。
- `Docker Daemon`作为Docker架构中的主体部分，首先提供Server的功能使其可以接受Docker Client的请求；
- `Engine`执行Docker内部的一系列工作，每一项工作都是以一个Job的形式的存在。
- `Job`的运行过程中，当需要容器镜像时，则从`Docker Registry`中下载镜像，并通过镜像管理驱动`graphdriver`将下载镜像以`Graph`的形式存储；
- 当需要为Docker创建网络环境时，通过网络管理驱动`networkdriver`创建并配置Docker容器网络环境；
- 当需要限制Docker容器运行资源或执行用户指令等操作时，则通过execdriver来完成。
- `libcontainer`是一项独立的容器管理包，`networkdriver`以及`execdriver`都是通过`libcontainer`来实现具体对容器进行的操作。

## Docker三要素

?>容器、镜像、Dockerfile是Docker的三要素，熟练掌握三者之间的转化，即掌握了Docker的基本使用。

<div align=left><img src="_images/docker/container-image-dockerfile.jpeg#pic_center" height="382" width="618"></div>

### Docker Containers
?>负责应用程序的`运行`，包括操作系统、用户添加的文件以及元数据。

### Docker Images
?>构建容器的`只读模板`，用来运行Docker容器

<div align=left><img src="_images/docker/docker-images.jpg#pic_center" height="618" width="618"></div>

### DockerFile
?>文件指令集，用来说明如何创建Docker镜像

## Docker三组件

### 一、Docker Client 
- Docker Client是和Docker Daemon建立通信的`客户端`。用户使用的可执行文件为docker（类似可执行脚本的命令），docker命令后接参数的形式来实现一个完整的请求命令（例如docker images，docker为命令不可变，images为参数可变）。
- Docker Client可以通过以下三种方式和Docker Daemon建立通信：`tcp://host:port`，`unix://path_to_socket`和`fd://socketfd`。
- Docker Client发送容器管理请求后，由Docker Daemon接受并处理请求，当Docker Client接收到返回的请求相应并简单处理后，Docker Client一次完整的生命周期就结束了。`一次完整的请求：发送请求→处理请求→返回结果`，与传统的C/S架构请求流程并无不同。

### 二、Docker Daemon

#### 2.1 Docker Daemon架构图
<div align=left><img src="_images/docker/docker-daemon.jpg#pic_center" height="610" width="618"></div>

#### 2.2 Docker Server 调度分发请求
<div align=left><img src="_images/docker/docker-server.jpg#pic_center" height="610" width="618"></div>

- 运行于主机上，处理服务请求
- Docker Server相当于C/S架构的服务端。功能为接受并调度分发Docker Client发送的请求。接受请求后，Server通过路由与分发调度，找到相应的Handler来执行请求。
- 在Docker的启动过程中，通过包gorilla/mux，创建了一个mux.Router，提供请求的路由功能。在Golang中，gorilla/mux是一个强大的URL路由器以及调度分发器。该mux.Router中添加了众多的路由项，每一个路由项由HTTP请求方法（PUT、POST、GET或DELETE）、URL、Handler三部分组成。
- 创建完mux.Router之后，Docker将Server的监听地址以及mux.Router作为参数，创建一个httpSrv=http.Server{}，最终执行httpSrv.Serve()为请求服务。
- 在Server的服务过程中，Server在listener上接受Docker Client的访问请求，并创建一个全新的goroutine来服务该请求。在goroutine中，首先读取请求内容，然后做解析工作，接着找到相应的路由项，随后调用相应的Handler来处理该请求，最后Handler处理完请求之后回复该请求。

#### 2.3 Docker Engine 

<div align=left><img src="_images/docker/docker-engine-components-flow.png#pic_center" height="382" width="618"></div>

- Engine是Docker架构中的运行引擎，同时也Docker运行的核心模块。它扮演Docker container存储仓库的角色，并且通过执行job的方式来操纵管理这些容器。
- 在Engine数据结构的设计与实现过程中，有一个handler对象。该handler对象存储的都是关于众多特定job的handler处理访问。举例说明，Engine的handler对象中有一项为：{“create”: daemon.ContainerCreate,}，则说明当名为"create"的job在运行时，执行的是daemon.ContainerCreate的handler。

#### 2.4 Docker Job
- 一个Job可以认为是Docker架构中Engine内部最基本的工作执行单元。Docker可以做的每一项工作，都可以抽象为一个job。例如：在容器内部运行一个进程，这是一个job；创建一个新的容器，这是一个job。
- Docker Server的运行过程也是一个job，名为serveapi。
- Job的设计者，把Job设计得与Unix进程相仿。比如说：Job有一个名称，有参数，有环境变量，有标准的输入输出，有错误处理，有返回状态等。

### 三、Docker Registry [镜像注册中心]
- Docker Registry是一个存储容器镜像的仓库（注册中心），可理解为云端镜像仓库，按repository来分类，docker pull 按照[repository]:[tag]来精确定义一个image。
- 在Docker的运行过程中，Docker Daemon会与Docker Registry通信，并实现搜索镜像、下载镜像、上传镜像三个功能，这三个功能对应的job名称分别为"search"，“pull” 与 “push”。
- 可分为公有仓库（docker hub）和私有仓库。

