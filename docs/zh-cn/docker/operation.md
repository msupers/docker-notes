# docker常用命令

##  软件信息

### docker --help

?> 列出docker可以用的命令和命令描述

```
ζ docker -h                                                                                                                                                                 
Flag shorthand -h has been deprecated, please use --help

Usage:	docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Options:
      --config string      Location of client config files (default "/home/zhangmiao334/.docker")
  -c, --context string     Name of the context to use to connect to the daemon (overrides DOCKER_HOST env var and default context set with "docker context use")
  -D, --debug              Enable debug mode
  -H, --host list          Daemon socket(s) to connect to
  -l, --log-level string   Set the logging level ("debug"|"info"|"warn"|"error"|"fatal") (default "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default "/home/zhangmiao334/.docker/ca.pem")
      --tlscert string     Path to TLS certificate file (default "/home/zhangmiao334/.docker/cert.pem")
      --tlskey string      Path to TLS key file (default "/home/zhangmiao334/.docker/key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            Print version information and quit

Management Commands:
  builder     Manage builds
  config      Manage Docker configs
  container   Manage containers
  context     Manage contexts
  engine      Manage the docker engine
  image       Manage images
  network     Manage networks
  node        Manage Swarm nodes
  plugin      Manage plugins
  secret      Manage Docker secrets
  service     Manage services
  stack       Manage Docker stacks
  swarm       Manage Swarm
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes

Run 'docker COMMAND --help' for more information on a command.
```

### docker version

?> Show the Docker version information *查看docker版本、运行平台等信息*

```shell
#Usage
ζ docker version --help                                                                                                                                                     

Usage:	docker version [OPTIONS]

Show the Docker version information

Options:
  -f, --format string       Format the output using the given Go template
      --kubeconfig string   Kubernetes config file

#Example
ζ docker version                                                                                                                                                            
Client:
 Version:           19.03.12-ce
 API version:       1.40
 Go version:        go1.14.5
 Git commit:        48a66213fe
 Built:             Sat Jul 18 01:33:21 2020
 OS/Arch:           linux/amd64
 Experimental:      false

Server:
 Engine:
  Version:          19.03.12-ce
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.14.5
  Git commit:       48a66213fe
  Built:            Sat Jul 18 01:32:59 2020
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          v1.4.0.m
  GitCommit:        09814d48d50816305a8e6c1a4ae3e2bcc4ba725a.m
 runc:
  Version:          1.0.0-rc92
  GitCommit:        ff819c7e9184c13b7c2607fe6c30ae19403a7aff
 docker-init:
  Version:          0.18.0
  GitCommit:        fec3683
```

### docker info

?> Display system-wide information *docker的详细信息，容器个数、状态、镜像数量、存储目录、仓库mirrors等*

```
#Usage
ζ docker info --help                                                                                                                                                        

Usage:	docker info [OPTIONS]

Display system-wide information

Options:
  -f, --format string   Format the output using the given Go template

#Example
ζ docker info                                                                                                                                                               
Client:
 Debug Mode: false

Server:
 Containers: 26
  Running: 0
  Paused: 0
  Stopped: 26
 Images: 377
 Server Version: 19.03.12-ce
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Native Overlay Diff: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 09814d48d50816305a8e6c1a4ae3e2bcc4ba725a.m
 runc version: ff819c7e9184c13b7c2607fe6c30ae19403a7aff
 init version: fec3683
 Security Options:
  apparmor
  seccomp
   Profile: default
 Kernel Version: 5.8.6-1-MANJARO
 Operating System: Manjaro Linux
 OSType: linux
 Architecture: x86_64
 CPUs: 8
 Total Memory: 7.472GiB
 Name: zhangmiao334-xdf
 ID: FWED:GFT7:WHBI:C4JE:DFTJ:74PR:NM3I:IKHQ:ZRL4:7GEI:LKQI:Q36G
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Registry Mirrors:
  https://hub-mirror.c.163.com/
  https://mirror.baidubce.com/
 Live Restore Enabled: false
```
## 镜像

### docker build

!>Build an image from a Dockerfile *通过Dockerfile制作一个镜像 --no-cache表示不使用缓存，--pull 表示Dockerfile中FROM的镜像每次都从远程拉取，避免使用本地旧数据.*

```shell
# Usage
docker build --help                                                                                                                                                       

Usage:	docker build [OPTIONS] PATH | URL | -

Build an image from a Dockerfile

Options:
      --add-host list           Add a custom host-to-IP mapping (host:ip)
      --build-arg list          Set build-time variables
      --cache-from strings      Images to consider as cache sources
      --cgroup-parent string    Optional parent cgroup for the container
      --compress                Compress the build context using gzip
      --cpu-period int          Limit the CPU CFS (Completely Fair Scheduler) period
      --cpu-quota int           Limit the CPU CFS (Completely Fair Scheduler) quota
  -c, --cpu-shares int          CPU shares (relative weight)
      --cpuset-cpus string      CPUs in which to allow execution (0-3, 0,1)
      --cpuset-mems string      MEMs in which to allow execution (0-3, 0,1)
      --disable-content-trust   Skip image verification (default true)
  -f, --file string             Name of the Dockerfile (Default is 'PATH/Dockerfile')
      --force-rm                Always remove intermediate containers
      --iidfile string          Write the image ID to the file
      --isolation string        Container isolation technology
      --label list              Set metadata for an image
  -m, --memory bytes            Memory limit
      --memory-swap bytes       Swap limit equal to memory plus swap: '-1' to enable unlimited swap
      --network string          Set the networking mode for the RUN instructions during build (default "default")
      --no-cache                Do not use cache when building the image
  -o, --output stringArray      Output destination (format: type=local,dest=path)
      --platform string         Set platform if server is multi-platform capable
      --progress string         Set type of progress output (auto, plain, tty). Use plain to show container output (default "auto")
      --pull                    Always attempt to pull a newer version of the image
  -q, --quiet                   Suppress the build output and print image ID on success
      --rm                      Remove intermediate containers after a successful build (default true)
      --secret stringArray      Secret file to expose to the build (only if BuildKit enabled): id=mysecret,src=/local/secret
      --security-opt strings    Security options
      --shm-size bytes          Size of /dev/shm
      --squash                  Squash newly built layers into a single new layer
      --ssh stringArray         SSH agent socket or keys to expose to the build (only if BuildKit enabled) (format: default|<id>[=<socket>|<key>[,<key>]])
      --stream                  Stream attaches to server to negotiate build context
  -t, --tag list                Name and optionally a tag in the 'name:tag' format
      --target string           Set the target build stage to build.
      --ulimit ulimit           Ulimit options (default [])

# Dockerfile内容如下
ζ cat Dockerfile                                                                                                                                                  
FROM dir.staff.xdf.cn/tess-dind/base:ubuntu-18.04
RUN apt-get install rsync -y
RUN wget http://mirror.bit.edu.cn/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz -O /tmp/apache-maven-3.6.3-bin.tar.gz
RUN tar -zxvf /tmp/apache-maven-3.6.3-bin.tar.gz -C /opt/ && rm -rf /tmp/apache-maven-3.6.3-bin.tar.gz 
COPY ./settings.xml /opt/apache-maven-3.6.3/conf/settings.xml
COPY ./kubectl /usr/bin/kubectl
COPY ./.kube /root/.kube
COPY ./mc /usr/bin/mc
COPY ./.mc /root/.mc
COPY ./.ssh /root/.ssh
ENV PATH $PATH:/opt/apache-maven-3.6.3/bin 
ENV MAVEN_HOME /opt/apache-maven-3.6.3

# Example
ζ docker build --no-cache --pull -t abcd .                                                                                                                       

Sending build context to Docker daemon  91.26MB
Step 1/12 : FROM dir.staff.xdf.cn/tess-dind/base:ubuntu-18.04
ubuntu-18.04: Pulling from tess-dind/base
Digest: sha256:649df2bc7fbd883e4ef4484d540fe08e8284286ab4dcd6351c10aecc8cbffa9f
Status: Image is up to date for dir.staff.xdf.cn/tess-dind/base:ubuntu-18.04
 ---> 7cbb329c91f1
Step 2/12 : RUN apt-get install rsync -y
 ---> Running in 7e96a1966946
Reading package lists...
Building dependency tree...
Reading state information...
The following additional packages will be installed:
  libpopt0
The following NEW packages will be installed:
  libpopt0 rsync
0 upgraded, 2 newly installed, 0 to remove and 5 not upgraded.
Need to get 361 kB of archives.
....

```

### docker images

?>List images *列出镜像列表，`SIZE`是解压后的大小，在registry存储的镜像要小得多。*

```shell
# Usage
ζ docker images --help                                                                                                                                                      

Usage:	docker images [OPTIONS] [REPOSITORY[:TAG]]

List images

Options:
  -a, --all             Show all images (default hides intermediate images)
      --digests         Show digests
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print images using a Go template
      --no-trunc        Don't truncate output
  -q, --quiet           Only show numeric IDs

# Excample
ζ docker images                                                                                                                                                             
REPOSITORY                                             TAG                   IMAGE ID            CREATED             SIZE
dir.staff.xdf.cn/tess-env/tomcat                       v9.0.36-jdk8          5fbb166fbd82        3 hours ago         700MB
<none>                                                 <none>                bf91dda17238        3 hours ago         673MB
dir.staff.xdf.cn/tess-dev/docs-center-docker           latest                e1d1447d8fdd        3 hours ago         605MB
dir.staff.xdf.cn/tess-dind/node                        ng-v6.2.9             a5264e598992        6 hours ago         1.33GB
dir.staff.xdf.cn/tess-dind/java                        jdk8-maven3.6.3       8aa74387d944        4 days ago          1.08GB
dir.staff.xdf.cn/tess-dind/node                        <none>                31a6c780f52d        4 days ago          1.31GB
dir.staff.xdf.cn/tess-dind/base                        ubuntu-18.04          7cbb329c91f1        4 days ago          992MB
dir.staff.xdf.cn/tess-dind/java                        <none>                a692df48dae4        12 days ago         1.07GB
dir.staff.xdf.cn/tess-dev/zm20200908-2                 latest                4f597b7ea366        12 days ago         672MB
......
```

### docker pull

?> Pull an image or a repository from a registry *从镜像仓库拉取镜像*

```shell
# Usage
ζ docker pull --help                                                                                                                                                        

Usage:	docker pull [OPTIONS] NAME[:TAG|@DIGEST]

Pull an image or a repository from a registry

Options:
  -a, --all-tags                Download all tagged images in the repository
      --disable-content-trust   Skip image verification (default true)
      --platform string         Set platform if server is multi-platform capable
  -q, --quiet                   Suppress verbose output

# Example
ζ docker pull dir.staff.xdf.cn/tess-dev/docs-center-docker:latest                                                                                                           

latest: Pulling from tess-dev/docs-center-docker
e9afc4f90ab0: Already exists 
989e6b19a265: Already exists 
af14b6c2f878: Already exists 
5573c4b30949: Already exists 
fb1a405f128d: Already exists 
197b0f525c26: Already exists 
f133ed18caca: Already exists 
a9e4d603b928: Already exists 
892b3200cbd0: Already exists 
c0fbeed62da4: Already exists 
f391c9809051: Already exists 
6c7aac71f510: Already exists 
c3298d5feb77: Already exists 
f41180d31ae8: Already exists 
ce5c3d22d92c: Already exists 
4da32586ae21: Pull complete 
9d0eff0df803: Pull complete 
Digest: sha256:ba7402a32d0d215d686c480f79f0161e12b81b38af8d7f5c9745e84fd18bf53d
Status: Downloaded newer image for dir.staff.xdf.cn/tess-dev/docs-center-docker:latest
dir.staff.xdf.cn/tess-dev/docs-center-docker:latest
```

### docker push

?>Push an image or a repository to a registry *向镜像仓库推送镜像*

```shell
# Usage
ζ docker push --help                                                                                                                                                        

Usage:	docker push [OPTIONS] NAME[:TAG]

Push an image or a repository to a registry

Options:
      --disable-content-trust   Skip image signing (default true)

# Example
ζ docker push dir.staff.xdf.cn/tess-dev/test-abc:latest                                                                                                                     
The push refers to repository [dir.staff.xdf.cn/tess-dev/test-abc]
210e87a70502: Layer already exists 
4d618beb43f4: Layer already exists 
55a2c6f191a6: Layer already exists 
081b2399e2f0: Layer already exists 
d1ad2e97aaf2: Layer already exists 
ce8c36b5e432: Layer already exists 
cf5afd617952: Layer already exists 
3ebf050c4a05: Layer already exists 
28ba7458d04b: Layer already exists 
838a37a24627: Layer already exists 
a6ebef4a95c3: Layer already exists 
b7f7d2967507: Layer already exists 
latest: digest: sha256:0e8a87ac526f0e09f09808e72b72799442bcf95cf0fe7c9913ec1cd35f91158c size: 2833
```

### docker tag

?>Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE  *给镜像定义别名*
```
# Usage
ζ docker tag --help                                                                                                                                                         

Usage:	docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]

Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE

# Example
ζ docker tag  dir.staff.xdf.cn/tess-dev/test-abc:latest  abcdefg:latest

ζ docker images |grep 2c4b481844a7                                                                                                                                       
dir.staff.xdf.cn/tess-dev/test-abc                     latest                2c4b481844a7        2 months ago        1.05GB
abcdefg                                                latest                2c4b481844a7        2 months ago        1.05GB

```

### docker rmi 

!> Remove one or more images *参数为镜像名称或镜像ID,删除镜像之前，请先删除使用此镜像运行的容器，否则会报错*

```
# Usage
ζ docker rmi --help                                                                                                                                                         

Usage:	docker rmi [OPTIONS] IMAGE [IMAGE...]

Remove one or more images

Options:
  -f, --force      Force removal of the image
      --no-prune   Do not delete untagged parents

# Example
ζ docker rmi abcdefg                                                                                                                                                        
Untagged: abcdefg:latest
#docker rmi by ID 
ζ docker rmi  2c4b481844a7                                                                                                                                                  
Error response from daemon: conflict: unable to delete 2c4b481844a7 (must be forced) - image is referenced in multiple repositories

```

### docker search

?>Search the Docker Hub for images *从官方的hub仓库查询镜像 OFFICIAL [OK] 表明是docker官方提供的镜像。*

```shell
# Usage
ζ docker search --help                                                                                                                                                      

Usage:	docker search [OPTIONS] TERM

Search the Docker Hub for images

Options:
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print search using a Go template
      --limit int       Max number of search results (default 25)
      --no-trunc        Don't truncate output

# Example      
ζ docker search ubuntu                                                                                                                                                      
NAME                                                      DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
ubuntu                                                    Ubuntu is a Debian-based Linux operating sys…   11331               [OK]                
dorowu/ubuntu-desktop-lxde-vnc                            Docker image to provide HTML5 VNC interface …   461                                     [OK]
rastasheep/ubuntu-sshd                                    Dockerized SSH service, built on top of offi…   247                                     [OK]
consol/ubuntu-xfce-vnc                                    Ubuntu container with "headless" VNC session…   226                                     [OK]
ubuntu-upstart                                            Upstart is an event-based replacement for th…   110                 [OK]                
neurodebian                                               NeuroDebian provides neuroscience research s…   70                  [OK]                
1and1internet/ubuntu-16-nginx-php-phpmyadmin-mysql-5      ubuntu-16-nginx-php-phpmyadmin-mysql-5          50                                      [OK]
ubuntu-debootstrap                                        debootstrap --variant=minbase --components=m…   44                  [OK]                

```
### docker inspect

?> Return low-level information on Docker objects *参数为容器名称 ID 或 镜像名称 ID。通过此命令可以查看详细信息，如环境变量，存储目录，容器的资源信息，状态信息等*

```shell
# Usage
ζ docker inspect --help                                                                                                                                                     

Usage:	docker inspect [OPTIONS] NAME|ID [NAME|ID...]

Return low-level information on Docker objects

Options:
  -f, --format string   Format the output using the given Go template
  -s, --size            Display total file sizes if the type is container
      --type string     Return JSON for specified type

# Example
ζ docker inspect dir.staff.xdf.cn/tess-env/jdk:v1.8.0-251                                                                                                                   
[
    {
        "Id": "sha256:a8cc74f68e51b2758b09fb2595063d37231eb0ef3f1ff902d3c96296f11753de",
        "RepoTags": [
            "dir.staff.xdf.cn/tess-env/jdk:v1.8.0-251",
            "dir.staff.xdf.cn/tess-pre/zm20200803-3:latest"
        ],
        "RepoDigests": [
            "dir.staff.xdf.cn/tess-env/jdk@sha256:f55c6e5304106ebf9fa7ade09f837302e84c03aee27ef350113f2936c730ba86"
        ],
        "Parent": "",
        "Comment": "",
        "Created": "2020-06-23T05:01:20.573341925Z",
        "Container": "8b47d3183341f2b6b81a0d08014fd8e779ddbf19f95143dc2fda5d71814d2d4c",
        "ContainerConfig": {
            "Hostname": "8b47d3183341",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/java/jdk1.8.0_251/bin",
                "JAVA_HOME=/opt/java/jdk1.8.0_251",
                "JRE_HOME=/opt/java/jdk1.8.0_251/jre",
                "CLASSPATH=.:/opt/java/jdk1.8.0_251/lib:/opt/java/jdk1.8.0_251/jre/lib"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "#(nop) ",
                "CMD [\"supervisord\"]"
            ],
            "Image": "sha256:03ab872f704c3b50d98181d4a54e3c7bb9609ff19682afbfbc3c504f852c8f98",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {}
        },
        "DockerVersion": "19.03.8",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/java/jdk1.8.0_251/bin",
                "JAVA_HOME=/opt/java/jdk1.8.0_251",
                "JRE_HOME=/opt/java/jdk1.8.0_251/jre",
                "CLASSPATH=.:/opt/java/jdk1.8.0_251/lib:/opt/java/jdk1.8.0_251/jre/lib"
            ],
            "Cmd": [
                "supervisord"
            ],
            "Image": "sha256:03ab872f704c3b50d98181d4a54e3c7bb9609ff19682afbfbc3c504f852c8f98",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": null
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 845773882,
        "VirtualSize": 845773882,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/568308cfd3eea8c041399683ccca5913e1b834e6f47c130fbe83837fd37a0e3a/diff:/var/lib/docker/overlay2/ef74e213dffe650c43f79265c82f00205a3c35118df2c7d2ce24bc44b82e3670/diff:/var/lib/docker/overlay2/b2e0f097cee9ad9fab9a671418df25da389ff61a1d0cb0e50ba488d9690f7a24/diff:/var/lib/docker/overlay2/6a2d15f55aea65faf595311c84375e7f56ae9b7b4debcd26a5f4e4161b9af77c/diff:/var/lib/docker/overlay2/3c89237512ff31abdb5c9a5f8f6adc87b27a5228c8df8a4f8230d15bfccf7ff7/diff:/var/lib/docker/overlay2/18280823bced67da095c4ac4f588c3bd1212350c77075a0dd5c762dc0c9caa63/diff",
                "MergedDir": "/var/lib/docker/overlay2/df7b156baa3c9e16a16629efc837d1bc1101b2a45692182870226c26702c1f7d/merged",
                "UpperDir": "/var/lib/docker/overlay2/df7b156baa3c9e16a16629efc837d1bc1101b2a45692182870226c26702c1f7d/diff",
                "WorkDir": "/var/lib/docker/overlay2/df7b156baa3c9e16a16629efc837d1bc1101b2a45692182870226c26702c1f7d/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:b7f7d2967507ba709dbd1dd0426a5b0cdbe1ff936c131f8958c8d0f910eea19e",
                "sha256:a6ebef4a95c345c844c2bf43ffda8e36dd6e053887dd6e283ad616dcc2376be6",
                "sha256:838a37a24627f72df512926fc846dd97c93781cf145690516e23335cc0c27794",
                "sha256:28ba7458d04b8551ff45d2e17dc2abb768bf6ed1a46bb262f26a24d21d8d7233",
                "sha256:266698974334b880024028f60a2aab818794b5260bff47fd74219d48b5184206",
                "sha256:595d1b26429f287f1dd2647e5a58932d3c7dde0988816aa21980e7ec07a4a29b",
                "sha256:97a3b6a34acb34d59a2192ab2d9b09843a1f5827a28a7d0d26a712a78eb43eaf"
            ]
        },
        "Metadata": {
            "LastTagTime": "2020-08-03T23:35:00.803274642+08:00"
        }
    }
]
```

## 容器

### docker ps

?>List containers *List 容器列表*

```shell
#!/bin/bash

# Usage
ζ docker ps --help                                                                                                                                                          

Usage:	docker ps [OPTIONS]

List containers

Options:
  -a, --all             Show all containers (default shows just running)
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print containers using a Go template
  -n, --last int        Show n last created containers (includes all states) (default -1)
  -l, --latest          Show the latest created container (includes all states)
      --no-trunc        Don't truncate output
  -q, --quiet           Only display numeric IDs
  -s, --size            Display total file sizes

# Example
ζ docker ps -a
CONTAINER ID        IMAGE                                                         COMMAND                  CREATED             STATUS                         PORTS                               NAMES
2105d82f1388        dir.staff.xdf.cn/tess-dind/java:jdk8-maven3.6.3               "bash"                   About an hour ago   Exited (1) About an hour ago                                       friendly_nobel
d786f8316020        registry.cn-beijing.aliyuncs.com/meowbite/sonar:7.9.2         "./bin/run.sh"           5 weeks ago         Up 3 weeks                                                         sonar-server
b45274f4c822        registry.cn-beijing.aliyuncs.com/meowbite/jfrog-jcr:7.4.3     "/entrypoint-artifac…"   5 weeks ago         Up 9 days                      0.0.0.0:8081-8082->8081-8082/tcp    b45274f4c822_jcr_jcr-test_1
9ef0729808ba        registry.cn-beijing.aliyuncs.com/meowbite/blueocean:v1.23.1   "/sbin/tini -- /usr/…"   5 weeks ago         Up 9 days                      50000/tcp, 0.0.0.0:8088->8080/tcp   jenkins-master
0305536f4ee5        nobodyiam/apollo-quick-start                                  "/apollo-quick-start…"   6 weeks ago         Exited (137) 3 weeks ago                                           apollo-quick-start
745b6558fa7e        mysql:5.7                                                     "docker-entrypoint.s…"   6 weeks ago         Exited (0) 3 weeks ago                                             apollo-db
3976ef8b1271        alpine:latest                                                 "/bin/sh"                6 weeks ago         Exited (0) 6 weeks ago                                             apollo-dbdata
1dd0c39d5073        mrjin/yapi:latest                                             "bash /wait-for-it.s…"   4 months ago        Exited (137) 3 months ago                                          yapi
d0f2f7aa26bf        mongo                                                         "docker-entrypoint.s…"   4 months ago        Exited (0) 3 months ago                                            mongo
50e0105cdb5b        ee085dd08494                                                  "supervisord"            4 months ago        Exited (0) 3 months ago 
```

### docker run

?>Run a command in a new container *从一个镜像启动一个容器，参数很多，常用的其实有限..*

```shell

# Usage
ζ docker  run --help                                                                                                                                                        

Usage:	docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

Run a command in a new container

Options:
      --add-host list                  Add a custom host-to-IP mapping (host:ip)
  -a, --attach list                    Attach to STDIN, STDOUT or STDERR
      --blkio-weight uint16            Block IO (relative weight), between 10 and 1000, or 0 to disable (default 0)
      --blkio-weight-device list       Block IO weight (relative device weight) (default [])
      --cap-add list                   Add Linux capabilities
      --cap-drop list                  Drop Linux capabilities
      --cgroup-parent string           Optional parent cgroup for the container
      --cidfile string                 Write the container ID to the file
      --cpu-period int                 Limit CPU CFS (Completely Fair Scheduler) period
      --cpu-quota int                  Limit CPU CFS (Completely Fair Scheduler) quota
      --cpu-rt-period int              Limit CPU real-time period in microseconds
      --cpu-rt-runtime int             Limit CPU real-time runtime in microseconds
  -c, --cpu-shares int                 CPU shares (relative weight)
      --cpus decimal                   Number of CPUs
      --cpuset-cpus string             CPUs in which to allow execution (0-3, 0,1)
      --cpuset-mems string             MEMs in which to allow execution (0-3, 0,1)
  -d, --detach                         Run container in background and print container ID
      --detach-keys string             Override the key sequence for detaching a container
      --device list                    Add a host device to the container
      --device-cgroup-rule list        Add a rule to the cgroup allowed devices list
      --device-read-bps list           Limit read rate (bytes per second) from a device (default [])
      --device-read-iops list          Limit read rate (IO per second) from a device (default [])
      --device-write-bps list          Limit write rate (bytes per second) to a device (default [])
      --device-write-iops list         Limit write rate (IO per second) to a device (default [])
      --disable-content-trust          Skip image verification (default true)
      --dns list                       Set custom DNS servers
      --dns-option list                Set DNS options
      --dns-search list                Set custom DNS search domains
      --domainname string              Container NIS domain name
      --entrypoint string              Overwrite the default ENTRYPOINT of the image
  -e, --env list                       Set environment variables
      --env-file list                  Read in a file of environment variables
      --expose list                    Expose a port or a range of ports
      --gpus gpu-request               GPU devices to add to the container ('all' to pass all GPUs)
      --group-add list                 Add additional groups to join
      --health-cmd string              Command to run to check health
      --health-interval duration       Time between running the check (ms|s|m|h) (default 0s)
      --health-retries int             Consecutive failures needed to report unhealthy
      --health-start-period duration   Start period for the container to initialize before starting health-retries countdown (ms|s|m|h) (default 0s)
      --health-timeout duration        Maximum time to allow one check to run (ms|s|m|h) (default 0s)
      --help                           Print usage
  -h, --hostname string                Container host name
      --init                           Run an init inside the container that forwards signals and reaps processes
  -i, --interactive                    Keep STDIN open even if not attached
      --ip string                      IPv4 address (e.g., 172.30.100.104)
      --ip6 string                     IPv6 address (e.g., 2001:db8::33)
      --ipc string                     IPC mode to use
      --isolation string               Container isolation technology
      --kernel-memory bytes            Kernel memory limit
  -l, --label list                     Set meta data on a container
      --label-file list                Read in a line delimited file of labels
      --link list                      Add link to another container
      --link-local-ip list             Container IPv4/IPv6 link-local addresses
      --log-driver string              Logging driver for the container
      --log-opt list                   Log driver options
      --mac-address string             Container MAC address (e.g., 92:d0:c6:0a:29:33)
  -m, --memory bytes                   Memory limit
      --memory-reservation bytes       Memory soft limit
      --memory-swap bytes              Swap limit equal to memory plus swap: '-1' to enable unlimited swap
      --memory-swappiness int          Tune container memory swappiness (0 to 100) (default -1)
      --mount mount                    Attach a filesystem mount to the container
      --name string                    Assign a name to the container
      --network network                Connect a container to a network
      --network-alias list             Add network-scoped alias for the container
      --no-healthcheck                 Disable any container-specified HEALTHCHECK
      --oom-kill-disable               Disable OOM Killer
      --oom-score-adj int              Tune host's OOM preferences (-1000 to 1000)
      --pid string                     PID namespace to use
      --pids-limit int                 Tune container pids limit (set -1 for unlimited)
      --platform string                Set platform if server is multi-platform capable
      --privileged                     Give extended privileges to this container
  -p, --publish list                   Publish a container's port(s) to the host
  -P, --publish-all                    Publish all exposed ports to random ports
      --read-only                      Mount the container's root filesystem as read only
      --restart string                 Restart policy to apply when a container exits (default "no")
      --rm                             Automatically remove the container when it exits
      --runtime string                 Runtime to use for this container
      --security-opt list              Security Options
      --shm-size bytes                 Size of /dev/shm
      --sig-proxy                      Proxy received signals to the process (default true)
      --stop-signal string             Signal to stop a container (default "SIGTERM")
      --stop-timeout int               Timeout (in seconds) to stop a container
      --storage-opt list               Storage driver options for the container
      --sysctl map                     Sysctl options (default map[])
      --tmpfs list                     Mount a tmpfs directory
  -t, --tty                            Allocate a pseudo-TTY
      --ulimit ulimit                  Ulimit options (default [])
  -u, --user string                    Username or UID (format: <name|uid>[:<group|gid>])
      --userns string                  User namespace to use
      --uts string                     UTS namespace to use
  -v, --volume list                    Bind mount a volume
      --volume-driver string           Optional volume driver for the container
      --volumes-from list              Mount volumes from the specified container(s)
  -w, --workdir string                 Working directory inside the container

# Example1 启动并进入一个容器的bash，退出时候删除该容器
ζ docker  run --rm -it dir.staff.xdf.cn/tess-env/tomcat:v9.0.36-jdk8 bash                                                                                                                            
root@10a91dd38271:/usr/local/tomcat# 

# Example2 后台启动一个容器
ζ docker run --name test -d  dir.staff.xdf.cn/tess-dev/docs-center-docker:latest                                                                                            
a0bbd8c95961ed7f6b2016b0fbdb8bfbd980f2ad7da53f870355ef112cd47631                                                                                                         
 
ζ docker ps |grep test                                                                                                                                                      
a0bbd8c95961        dir.staff.xdf.cn/tess-dev/docs-center-docker:latest   "docsify serve . --p…"   14 seconds ago       Up 13 seconds       8080/tcp            test

```

### docker start

?>Start one or more stopped containers *将一个关闭着的容器启动*

```shell

# Usage

ζ docker  start --help                                                                                                                                                      

Usage:	docker start [OPTIONS] CONTAINER [CONTAINER...]

Start one or more stopped containers

Options:
  -a, --attach                  Attach STDOUT/STDERR and forward signals
      --checkpoint string       Restore from this checkpoint
      --checkpoint-dir string   Use a custom checkpoint storage directory
      --detach-keys string      Override the key sequence for detaching a container
  -i, --interactive             Attach container's STDIN

# Example

## stop 容器
ζ docker stop test                                                                                                                                                          
test
## -a 查看退出容器状态
ζ docker ps -a|grep test                                                                                                                                                    
a0bbd8c95961        dir.staff.xdf.cn/tess-dev/docs-center-docker:latest        "docsify serve . --p…"   5 minutes ago       Exited (137) 14 seconds ago                       test
## start 容器
ζ docker start test                                                                                                                                                         
test
## 查看容器状态
ζ docker ps |grep test                                                                                                                                                      
a0bbd8c95961        dir.staff.xdf.cn/tess-dev/docs-center-docker:latest   "docsify serve . --p…"   5 minutes ago       Up 5 seconds        8080/tcp            test
```

### docker exec

?>Run a command in a running container *从主机直接操作容器里的命令*

```bash
# Usage
ζ docker exec --help                                                                                                                                                        

Usage:	docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

Run a command in a running container

Options:
  -d, --detach               Detached mode: run command in the background
      --detach-keys string   Override the key sequence for detaching a container
  -e, --env list             Set environment variables
  -i, --interactive          Keep STDIN open even if not attached
      --privileged           Give extended privileges to the command
  -t, --tty                  Allocate a pseudo-TTY
  -u, --user string          Username or UID (format: <name|uid>[:<group|gid>])
  -w, --workdir string       Working directory inside the container

# Example
## 去容器里执行命令，执行完毕还是在主机的shell里
ζ docker exec -it a0bbd8c95961 cat /etc/issue                                                                                                                               
Debian GNU/Linux 10 \n \l

ζ docker exec -it a0bbd8c95961 cat /etc/os-release                                                                                                                          
PRETTY_NAME="Debian GNU/Linux 10 (buster)"
NAME="Debian GNU/Linux"
VERSION_ID="10"
VERSION="10 (buster)"
VERSION_CODENAME=buster
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"

## 进入容器的bash环境，相当于登录到容器里 
ζ docker exec -it a0bbd8c95961 bash                                                                                                                                         
root@a0bbd8c95961:/user/local/docs# ls
README.md  _images  _media  _sidebar.md  index.html  zh-cn
```

### docker cp

?>Copy files/folders between a container and the local filesystem

### docker stats

?>Display a live stream of container(s) resource usage statistics

```
Usage
ζ docker stats --help                                                                                                                                                       

Usage:	docker stats [OPTIONS] [CONTAINER...]

Display a live stream of container(s) resource usage statistics

Options:
  -a, --all             Show all containers (default shows just running)
      --format string   Pretty-print images using a Go template
      --no-stream       Disable streaming stats and only pull the first result
      --no-trunc        Do not truncate output
```
<div align=left><img src="../../_images/docker/docker-stats-example.gif#pic_center" height="382" width="618""></div>

### docker top

?>Display the running processes of a container *从主机查看容器里的进程*
```shell
# Usage
ζ docker top --help                                                                                                                                                         

Usage:	docker top CONTAINER [ps OPTIONS]

Display the running processes of a container

# Example
ζ docker top test                                                                                                                                                           
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                66324               66306               0                   19:24               ?                   00:00:00            node /usr/local/bin/docsify serve . --port 8080
```


