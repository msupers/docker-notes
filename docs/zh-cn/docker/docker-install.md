# 安装Docker

- The **overlay2** storage driver is recommended.
- xfs ftype=1  

## Centos上安装
<div align=left><img src="_images/install/centos-logo.jpg#pic_center" height="382" width="618"></div>

!>**卸载旧版本（前提是通过yum安装过，并且期望卸载时）**

```shell
$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

### 通过yum安装

- Install the yum-utils package (which provides the yum-config-manager utility) and set up the stable repository.

```shell
sudo yum install -y yum-utils
```

- 配置docker-ce的yum源

```shell
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

- 安装latest version
```shell
sudo yum install docker-ce docker-ce-cli containerd.io
```

- list aviable version
```shell
yum list docker-ce --showduplicates | sort -r
```
```shell
docker-ce.x86_64  3:18.09.1-3.el7                     docker-ce-stable
docker-ce.x86_64  3:18.09.0-3.el7                     docker-ce-stable
docker-ce.x86_64  18.06.1.ce-3.el7                    docker-ce-stable
docker-ce.x86_64  18.06.0.ce-3.el7                    docker-ce-stable
```

- install 特定的版本
```shell
sudo yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io
```

### 通过二进制安装

?>核心思想是把bin文件放到bin目录，配置文件放到配置文件目录，然后启动服务。具体做法如下：

- 创建一个安装脚本 *如docker-install.sh ，然后拉取二进制包，然后执行脚本。*

```shell
#!/bin/bash
usage(){
  echo "Usage: $0 FILE_NAME_DOCKER_CE_TAR_GZ"
  echo "       $0 docker-18.09.0-ce.tgz"
  echo "Get docker-ce binary from: https://download.docker.com/linux/static/stable/x86_64/"
  echo "eg: wget https://download.docker.com/linux/static/stable/x86_64/docker-17.09.0-ce.tgz"
  echo "" 
}

# Vars
SYSTEMDDIR=/usr/lib/systemd/system
SERVICEFILE=docker.service
DOCKERDIR=/usr/bin
DOCKERBIN=docker
SERVICENAME=docker

# check installed status
which docker

if [ $? -eq 0 ];then
  echo "Pls uninstall  docker first, then start install"
  exit
fi

# Var nums check
if [ $# -ne 1 ];then
  usage
  exit 1
else
  FILETARGZ="$1"
fi

if [ != ${FILETARGZ} ];then
  echo "Docker binary tgz files does not exist, please check it"
  echo "Get docker-ce binary from: https://download.docker.com/linux/static/stable/x86_64/"
  echo "eg: wget https://download.docker.com/linux/static/stable/x86_64/docker-18.09.0.tgz"
fi

echo "## step1, unzip: tar -zxvf ${FILETARGZ}"
tar -zxvf ${FILETARGZ}

echo "## step2, binary :copy  ${DOCKERBIN} to ${DOCKERDIR}"
cp -p ${DOCKERBIN}/* ${DOCKERDIR} >/dev/null 2>&1
which ${DOCKERBIN}  
echo "## step3, systemd service: create docker systemd file,  ${SERVICEFILE}"
cat >${SYSTEMDDIR}/${SERVICEFILE} <<EOF
[Unit]
Description=Docker Application Container Engine
Documentation=http://docs.docker.com
After=network.target docker.socket
[Service]
Type=notify
WorkingDirectory=/usr/local/bin
ExecStart=/usr/bin/dockerd --storage-opt overlay2.override_kernel_check=1  --storage-driver=overlay2 --graph=/data/docker_rt \
                --selinux-enabled=false \
                --log-opt max-size=1g
ExecReload=/bin/kill -s HUP $MAINPID
# Having non-zero Limit*s causes performance problems due to accounting overhead
# in the kernel. We recommend using cgroups to do container-local accounting.
# Uncomment TasksMax if your systemd version supports it.
LimitNOFILE=1000000
LimitNPROC=100000
LimitCORE=102400000000
LimitSTACK=104857600
LimitSIGPENDING=600000
# Only systemd 226 and above support this version.
#TasksMax=infinity
TimeoutStartSec=0
# set delegate yes so that systemd does not reset the cgroups of docker containers
Delegate=yes
# kill only the docker process, not all processes in the cgroup
KillMode=process
Restart=on-failure
[Install]
WantedBy=multi-user.target
EOF

echo ""

systemctl daemon-reload

echo "step4 check install status:"
systemctl status ${SERVICENAME}
echo "##Service restart: ${SERVICENAME}"
systemctl restart ${SERVICENAME}
echo "##Service status: ${SERVICENAME}"
systemctl status ${SERVICENAME}

echo "##Service enabled: ${SERVICENAME}"
systemctl enable ${SERVICENAME}

echo "## docker version"
docker version
```
- 下载二进制包,和docker-install.sh脚本同一个目录

```shell
wget https://download.docker.com/linux/static/stable/x86_64/docker-<VERSION_STRING>.tgz
```

- 执行脚本

```shell
sh -x docker-install.sh  docker-<VERSION_STRING>.tgz
```

## Ubuntu上安装

### 卸载旧版本

- 旧版本的Docker命名为`docker`或`docker-engine`，如果有安装旧版本，先卸载旧版本

```shell
sudo apt-get remove docker docker-engine docker.io
```

### 配置repo

- 升级apt

```shell
sudo apt-get update
```

- 允许apt使用https

```shell
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
```

- 添加Docker 官方的GPG密钥

```shell
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

- 添加Docker软件源

```shell
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

### 安装Docker

```shell
sudo apt-get update
```
```shell
sudo apt-get install docker-ce
```

### 启动Docker

```shell
sudo systemctl enable docker   #设置开机启动
```

```shell
sudo systemctl start docker #启动Docker
```

