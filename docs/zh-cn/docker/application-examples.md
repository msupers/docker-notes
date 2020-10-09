# Docker应用实例
?>docker + CICD工具 + 容器编排工具 具有数量可观的玩法。<br/>本文总结典型使用，抛砖引玉......

## docker-compose举例

### 部署jenkins master

?> docker+docker-compose

- docker-compose在单机上编排容器，实现`数据持久化`，网络、资源、端口、开机启动等管理。

```
version: '3'
services:
    jenkins-blueocean:
        #jenkins master镜像
        image: "registry.cn-beijing.aliyuncs.com/meowbite/blueocean:v1.23.1"
        container_name: "jenkins-master"
        restart: always
        volumes:
            - ./jenkins_home:/var/jenkins_home
            - /run/docker.sock:/run/docker.sock
        ports:
            - 8088:8080
        networks:
           extnetwork:
networks:
   extnetwork:
      ipam:
         config:
         - subnet: 192.168.168.0/24
```

## docker在jenkins上的使用

### jenkins动态slave

?>docker + CICD

- 使用给定的容器执行流水线或阶段。
- 该容器将在预置的 node上，或在匹配可选定义的`label` 参数上，动态的供应来接受基于Docker的流水线。 
- docker 也可以选择的接受 args 参数，该参数可能包含直接传递到 docker run 调用的参数, 以及 alwaysPull 选项, 该选项强制 docker pull ，即使镜像名称已经存在。 

```shell
Jenkinsfile (Declarative Pipeline)
pipeline {
    agent { docker 'maven:3-alpine'
            label "$T_AGENT_LABEL"
            alwaysPull true
            args '-v /neworiental/maven-local-repo:/root/.m2 -v /run/docker.sock:/run/docker.sock'
     } 
    stages {
        stage('Example Build') {
            steps {
                sh 'mvn -B clean verify'
            }
        }
    }
}
```

## docker在k8s上的使用

### 在k8s上使用docker部署服务
?>docker + k8s + service

- 容器的高可用：负载均衡
- 容器横向扩缩容： 调整容器的数量
- 容器的纵向扩缩容：调整容器的配置
- 举例
    - Deployment yaml 示例
```shell
apiVersion: apps/v1 
kind: Deployment
metadata:
  name: ${SUBPROJECT_NAME}
  labels:
    app: ${SUBPROJECT_NAME}
  namespace: ${NAMESPACE}
spec:
  selector:
    matchLabels:
      app: ${SUBPROJECT_NAME}
  # 启动几个pod数量
  replicas: 0
  template:
    metadata:
      labels:
        app: ${SUBPROJECT_NAME}
    spec:
      containers:
      - name: ${SUBPROJECT_NAME}
        # 使用的docker镜像
        image: dir.staff.xdf.cn/${TESS_ENV}/${SUBPROJECT_NAME}
        ports:
        - containerPort: ${SERVICE_PORT}
        # docker的cpu 和内存字眼限制
        resources:
          limits:
            cpu: "${CPU}"
            memory: ${MEM}Gi
```
    - Service yaml 示例

```shell
apiVersion: v1
# 给多个容器分配一个虚拟IP，使用这个IP作为服务的入口（容器个数可以自由变化，请求入口不变），实现访问的高可用
kind: Service
metadata:
    name: ${SUBPROJECT_NAME}
    namespace: ${NAMESPACE}
spec:
    ports:
      - port: ${SERVICE_PORT}
        targetPort: ${SERVICE_PORT}
        protocol: TCP
    type: NodePort
    selector:
        app: ${SUBPROJECT_NAME}

```
    - 访问服务
```shell
ζ kubectl get service service-example                                                                                                   
NAME                 TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
service-example        NodePort   172.24.116.248   <none>        80:30875/TCP   42h

# CLUSTER-IP是虚拟IP，提供高可用
```





