## Linux安装

**安装方式介绍**

物理机安装：直接将操作系统安装到服务器硬件上

虚拟机安装：通过虚拟机软件安装

**安装Linux**

![](images/Snipaste_2024-10-27_22-27-07.png)

**网卡设置**

由于启动服务器时未加载网卡,导致IP地址初始化失败

![](images/Snipaste_2024-10-27_22-32-35.png)

修改网络初始化配置,设定网卡在系统启动时初始化

```
cd /				进入根目录
cd etc				进入etc目录
cd sysconfig		进入sysconfig目录
cd network-scripts	进入network-scripts
vi ifcfg-ens33		编辑ifcfg-ens33文件
```

![](images/Snipaste_2024-10-27_22-36-49.png)

**安装SSH连接工具**

![](images/Snipaste_2024-10-27_22-46-26.png)

## Linux常用命令

## Linux软件安装

## Linux项目部署

