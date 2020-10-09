# 虚拟化基础

?> 初学者经常搞不清楚，`虚拟化`、`容器`、以及`Docker`之间的关系。<br/>通过本文将快速了解它们。

## 虚拟化概念

- 计算机资源的抽象
    - 一个物理资源 >> 多个虚拟资源 *通常所说的虚拟机属于这一种*
    <div align=left><img src="_images/virtualization/p2v2.png#pic_center" height="382" width="618""></div>
    - 多个物理资源 >> 一个虚拟资源
    <div align=left><img src="_images/virtualization/p2v1.png#pic_center" height="382" width="618""></div>
- 抽象资源的类型
    - CPU 、内存 、磁盘 、网络 ......

## 虚拟化类型

- OS级别虚拟化
- 桌面虚拟化
- **`硬件虚拟化`**
    - 在使用`体验上`虚拟机和物理机几乎`没有差异`，如：虚拟机里可以看到`“自己的”`CPU、内存、网卡等硬件信息
- 硬件辅助虚拟化
    - 借助包含专门支持虚拟化技术的CPU硬件进行虚拟化操作，可以提高硬件虚拟化的性能

## 硬件虚拟化概念

- 宿主机：运行虚拟化软件的`物理机`
- 客户机：在物理机器上虚拟化出来`虚机`
- Hypervisor/virtual machine monitor
    - 在宿主机上创建、监测和管理虚拟机的`软件`或`系统`，如VMWARE的ESXi、Vcenter等
- Hypervisor类型-Bare-metal(裸金属)
    - 直接运行在物理`裸机`上，对机器拥有绝对的控制权
    - `非`传统的linux操作系统 *而是根据linux系统改装的操作系统及软件*
    <div align=left><img src="../../_images/virtualization/virtualization-3.png#pic_center" height="382" width="618""></div>
- Hypervisor类型-hosted
    - 运行在`宿主机的操作系统`之上
    - 一般为操作系统内核模块
    - 很多虚拟化功能依赖于操作系统本身功能或专门硬件功能
    <div align=left><img src="../../_images/virtualization/virtualization-4.png#pic_center" height="382" width="618"></div>

## 硬件虚拟化优缺点

- 优势
    - 提供`完整`机器的模拟，含各种设备：存储、网络等
    - 提供完整的操作系统，`独立的内核`
    - 和容器相比，`隔离性好`

- 不足
    - 虚拟化栈复杂
    - 软件功能重复
    - `性能损耗`，虚拟机里的硬件，是虚拟出来的，不是直接访问服务器的硬件
<!-- <div align=left><img src="../../_images/virtualization/virtualization-5.png#pic_center" height="382" width="618"></div> -->

## Linux Container（LXC）
?>LXC是Linux内核容器虚拟化的一项技术，可以实现资源的`隔离`和`控制`，也就是对`Cgroup`和`Namespace`两个属性的控制。

- 轻量级的内核虚拟化技术
- 在单一主机上提供多个虚拟环境（容器）`隔离进程`和资源，每个虚拟环境拥有自己的进程和`独立的`网络空间
- 将单个操作系统管理的资源划分到孤立的组，在不同组间平衡有冲突的资源使用需求
- 从用户角度看，容器和独立运行一台Linux一样
- 容器技术原理
    - 使用`Cgroup`迚行`资源限制`
    - 使用`Namespace`迚行`资源隔离`

## Docker
?>`早期`基于`LXC`技术创建的容器引擎，实现`Cgroup`和`Namespace`的`控制` <br/>`现在`使用`libcontainer`(golang的库)实现`Cgroup`和`Namespace`的`控制`，消除了对LXC的依赖。

<div align=left><img src="../../_images/docker/docker-architecture.svg#pic_center" width="70%"></div>

- 目标
    - `减化`环境管理`复杂度`，减化应用实例部署工作，将应用打成Image部署 *如官网所述：Package Software into Standardized Units for Development, Shipment and Deployment*
        - OS 如：Debian、Centos、Ubuntu等`操作系统`，开箱即用
        - 中间件 如： Mysql、nginx、Kafka、Zookeeper等中间件`软件`，开箱即用
        - 复杂环境 如：Hadoop、ELK、Harbor等`集群`，开箱即用
        - 微服务 如前端web、后端API等`服务`，开箱即用
    - 提供`轻量`级虚拟化技术
        - docker容器本质是`进程`，硬件资源、内核都是直接访问主机的，效率很高
    - 在CI/CD过程中提供`交付`的`标准化`管理。使<a onclick="window.open('https://www.jacoco.org/jacoco/')"/>DevOps</a>有了`革命性`的进展。
        - 各种App *web、api等服务，高效地进行快速打包，运输、部署、扩容、缩容、迁移*

## Docker与硬件虚拟化对比

?>与硬件虚拟化相比，具有性能优势

<div align=left><img src="../../_images/docker/docker-vs-vm-official.png#pic_center" width="70%"></div>

| 特性 | Docker | 虚拟机 | 
| :---------- |:------------| :-----------|
|启动速度          |秒级                      |分钟级          |
|磁盘使用          |MB                       |GB          |
|性能              |接近native               |有性能损失          | 
|系统支持量         |单机支持上千个容器         |一般十几个          |
|隔离性            |安全隔离                  |完全隔离          |



