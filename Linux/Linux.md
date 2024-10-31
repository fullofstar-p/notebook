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

| 命令           | 对应英文             | 作用                    |
| -------------- | -------------------- | ----------------------- |
| ls             | list                 | 查看当前目录下的内容    |
| pwd            | print work directory | 查看当前所在目录        |
| cd [目录名]    | change directory     | 切换目录                |
| touch [文件名] | touch                | 如果文件不存在,新建文件 |
| mkdir [目录名] | make directory       | 创建目录                |
| rm [文件名]    | remove               | 删除指定文件            |

### **Linux命令使用技巧**

- Tab键自动补全

- 连续两次Tab键,给出操作提示

- 使用上下箭头快速调出曾经使用过的命令

- 使用clear命令或Ctrl+l快捷键实现清屏

### **Linux命令格式**

`command [-options] [parameter]`

说明:

- command:命令名

- [-options]:选项,可用来对命令进行控制,也可以省略

- [parameter]:传给命令的参数,可以是零个,一个或多个

注意:

- []代表可选
- 命令名、选项、参数之间有空格进行分割

**文件目录操作命令==ls==**

作用：显示指定目录下的内容

语法：`ls [-al] [dir]`

说明:

- -a 显示所有文件及目录(.开头的隐藏文件也会列出)
- -l除文件名称外,同时将文件型态(d表示目录,-表示文件)、权限、拥有者、文件大小等信息详细列出

注意：

`ls -l 可简写为 ll`

### **文件目录操作命令==cd==**

作用：用于切换当前工作目录，即进入指定目录

语法：`cd [dirName]`

特殊说明：

- ~表示用户的home目录
- .表示目前所在的目录
- ..表示目前所在目录位置的上级目录

### **文件目录操作命令==cat==**

作用：用于显示文件内容

语法:`cat [-n] fileName`

说明:

- -n：由1开始对所有输出的行数编号

### **文件目录操作命令==more==**

作用：以分页的形式显示文件内容

语法：`more fileName`

操作说明:

- 回车键	向下滚动一行
- 空格键        向下滚动一屏
- b                 返回上一屏
- q或者Ctrl+C 退出more

### **文件目录操作命令==tail==**

作用:查看文件末尾的内容

语法：`tail [-f] fileName`

说明:

- -f:动态读取文件末尾内容并显示,通常用于日志文件的内容输出

举例:

`tail -20 /etc/profile		显示文件末尾20行的内容`

`tail -f /itcast/my.log		动态读取文件末尾内容并显示`

### **文件目录操作命令==mkdir==**

作用:创建目录

语法：`mkdir [-p] dirName`

说明:

- -p:确保目录名称存在,不存在的就创建一个。通过此选项，可以实现多层目录同时创建

### **文件目录操作命令==r mdir==**

作用：删除空目录

语法：`rmdir [-p] dirName`

说明：

- -p：当子目录被删除后使父目录为空目录的话，则一并删除

### **文件目录操作命令==r m==**

作用：删除文件或者目录

语法：`rm [-rf] name`

说明:

- -r：将目录及目录中所有文件（目录）逐一删除，即递归删除
- -f：无需确认，直接删除

### **拷贝移动命令==cp==**

作用：用于复制文件或者目录

语法：`cp [-r] source dest`

说明：

- -r：如果复制的是目录需要使用此选项，此时将复制该目录下所有的子目录和文件

### **拷贝移动命令==mv==**

作用：为文件或者目录改名、或将文件或者目录移动到其他位置

语法：`mv source dest`

### **打包压缩命令==tar==**

作用：对文件进行打包、解包、压缩、解压

语法：`tar [-zcxvf] fileName [files]`

包文件后缀为==.tar==表示只是完成了打包，并没有压缩

包文件后缀为==.tar.gz==表示打包的同时还进行了压缩

说明：

- -z：z代表的是gzip，通过gzip命令处理文件，gzip可以对文件压缩或者解压
- -c：c代表的是create，即创建新的包文件
- -x：x代表的是extract，实现从包文件中还原文件
- -v：v代表的是verbose，显示命令的执行过程
- -f：f代表的是file，用于指定包文件的名称
- -C：指定解压目录

### **文本编辑命令==vi/vim==**

作用：vi命令是Linux系统提供的一个文本编辑工具，可以对文件内容进行编辑，类似于Windows中的记事本

语法：`vi fileName`

针对vim中的三种模式说明如下：

1. 命令模式
   - 命令模式下可以查看文件内容、移动光标（上下左右箭头、gg、G）
   - 通过vim命令打开文件后，默认进入命令模式
   - 另外两种模式需要首先进入命令模式，才能进入彼此
2. 插入模式
   - 插入模式下可以对文件内容进行编辑
   - 在命令模式下按`[i,a,o]`任意一个，可以进入插入模式。进入插入模式后，下方会出现`[insert]`字样
   - 在插入模式下按`ESC`键,回到命令模式
3. 底行模式
   - 底行模式下可以通过命令对文件内容进行查找、显示行号、退出等操作
   - 在命令模式下按`[: /]`任意一个,可以进入底行模式
   - 通过`/`方式进入底行模式后,可以对文件内容进行查找
   - 通过`:`方式进入底行模式后,可以输入`wq (保存并退出)`、`q!(不保存退出)`、`set nu (显示行号)`

### **查找命令==find==**

作用：在指定目录下查找文件

语法：`find dirName -option fileName`

### **查找命令==grep==**

作用：从指定文件中查找指定的文本内容

语法：`grep word fileName`

## Linux软件安装

**软件安装方式**

- 二进制发布包安装

  软件已经针对具体平台编译打包发布，只要解压，修改配置即可

- rpm安装

  软件已经按照redhat的包管理规范进行打包，使用rpm命令进行安装，不能自行解决库依赖问题

- yum安装

  一种在线软件安装方式，本质还是rpm安装，自动下载安装包并安装，安装过程中自动解决库依赖问题

- 源码编译安装

  软件以源码工程的形式发布，需要自己编译打包

### **安装jdk**

1. 使用FinalShell自带的上传工具将jdk的二进制发布包上传到Linux

2. 解压安装包，命令为tar -zxvf jdk-8u171-linux-x64.tar.gz-C /usr/local

3. 配置环境变量，使用vim命令修改／etc/profile文件，在文件末尾加入如下配置
   JAVA_HOME=/usr/local/jdk1.8.0_171

   PATH=`$JAVA_HOME/bin:$PATH`

4. 重新加载profile文件，使更改的配置立即生效，命令为source /etc/profile

5. 检查安装是否成功，命令为java-version

### **安装Tomcat**

1. 使用FinalShell自带的上传工具将Tomcat的二进制发布包上传到Linux
2. 解压安装包，命令为tar-zxvf apache-tomcat-7.0.57.tar.gz -C /usr/local
3. 进入Tomcat的bin目录启动服务，命令为sh startup.sh或者．/startup.sh

**验证Tomcat启动是否成功,有多种方式:**

- 查看启动日志

  `more /usr/local/apache-tomcat-7.0.57/logs/catalina.out`

  `tail-50 /usr/local/apache-tomcat-7.0.57/logs/catalina.out`

- 查看进程

  ==ps -ef | grep tomcat==

==注意==:

- ==ps==命令是linux下非常强大的进程查看命令，通过==ps -ef==可以查看当前运行的所有进程的详细信息
- =="I"==在Linux中称为管道符，可以将前一个命令的结果输出给后一个命令作为输入
- 使用ps命令查看进程时，经常配合管道符和查找命令 grep 一起使用，来查看特定进程

**防火墙操作**

- 查看防火墙状态（systemctl status firewalld、firewall-cmd --state)
- 暂时关闭防火墙（systemctl stop firewalld)
- 永久关闭防火墙（systemctl disable firewalld)
- 开启防火墙（systemctl start firewalld)
- 开放指定端口（firewall-cmd --zone=public --add-port=8080/tcp --permanent)
- 关闭指定端口（firewall-cmd --zone=public --remove-port=8080/tcp --permanent)
- 立即生效（firewall-cmd --reload)
- 查看开放的端口（firewall-cmd --zone=public --list-ports)

==注意==:

1. systemctl是管理Linux中服务的命令，可以对服务进行启动、停止、重启、查看状态等操作
2. firewall-cmd是Linux中专门用于控制防火墙的命令
3. 为了保证系统安全，服务器的防火墙不建议关闭

**停止Tomcat服务的方式**

- 运行Tomcat的bin目录中提供的停止服务的脚本文件

  `sh shutdown.sh`

  `./shutdown.sh`

- 结束Tomcat进程

  查看Tomcat进程，获得进程id

  执行命令结束进程`kill -9 7742`

==注意==

kill命令是Linux提供的用于结束进程的命令，-9表示强制结束

### **安装MySQL**

1. 检测当前系统中是否安装MySQL数据库

   ```Linux
   rpm-qa				   查询当前系统中安装的所有软件
   rpm-qa |grep mysql		查询当前系统中安装的名称带mysql的软件
   rpm -qa | grep mariadb	查询当前系统中安装的名称带mariadb的软件
   ```

   RPM(Red-Hat Package Manager)RPM软件包管理器，是红帽Linux用于管理和安装软件的工具

   ==注意事项==
   如果当前系统中已经安装有MySQL数据库，安装将失败。CentOS7自带mariadb，与MySQL数据库冲突

2. 卸载已经安装的冲突软件

   ```Linux
   rpm -e --nodeps 软件名称								卸载软件
   rpm -e --nodeps mariadb-libs-5.5.60-1.el7_5.x86_64
   ```

3. 将资料中提供的MySQL安装包上传到Linux并解压

   ```Linux
   mkdir /usr/local/mysql
   tar -zxvf mysql-5.7.25-1.el7.x86_64.rpm-bundle.tar.gz -C /usr/local/mysql
   ```

4. 按照顺序安装rpm软件包

   ```Linux
   rpm -ivh mysql-community-common-5.7.25-1.el7.x86_64.rpm
   rpm -ivh mysql-community-libs-5.7.25-1.el7.x86_64.rpm 
   rpm -ivh mysql-community-devel-5.7.25-1.el7.x86_64.rpm 
   rpm -ivh mysql-community-libs-compat-5.7.25-1.el7.x86_64.rpm 
   rpm -ivh mysql-community-client-5.7.25-1.el7.x86_64.rpm 
   
   说明1：安装过程中提示缺少net-tools依赖，使用yum安装
   yum install net-tools
   
   rpm -ivh mysql-community-server-5.7.25-1.el7.x86_64.rpm
   
   说明2：可以通过指令升级现有软件及系统内核
   yum update
   ```

5. 启动mysql

   ```Linux
   systemctl status mysqld		查看mysql服务状态
   systemctl start mysqld		启动mysql服务
   
   说明：可以设置开机时启动mysql服务，避免每次开机启动mysql
   
   systemctl enable mysqld		开机启动mysql服务
   netstat -tunlp				查看已经启动的服务
   netstat -tunlp | grep mysql
   
   ps -ef | grep mysql			查看mysql进程
   ```

6. 登录MySQL数据库，查阅临时密码

   ```Linux
   cat /var/log/mysqld.log						查看文件内容
   cat /var/log/mysqld.log | grep password		  查看文件内容中包含password的行信息
   ```

   ==注意事项==

   冒号后面的是密码，注意空格

7. 登录MySQL，修改密码，开放访问权限

   ```
   mysql -uroot -p							  登录mysql（使用临时密码登录）
   ＃修改密码
   set global validate_password_length=4;		设置密码长度最低位数
   set global validate_password_policy=LOW;	设置密码安全等级低，便于密码可以修改成root 
   set password = password('root');			设置密码为root
   ＃开启访问权限
   grant all on *.* to 'root'@'%' identified by 'root';
   flush privileges;
   ```

8. 测试MySQL数据库是否正常工作

   ```
   show databases;
   ```

### **安装lrzsz**

**操作步骤**

1. 搜索lrzsz安装包，命令为`yum list lrzsz`
2. 使用yum命令在线安装，命令为`yum install lrzsz.x86_64`

==注意事项==

Yum（全称为 Yellow dog Updater, Modified）是一个在Fedora和RedHat以及CentOS中的Shell前端软件包管理器。基于RPM包管理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖关系，并且一次安装所有依赖的软件包，无须繁琐地一次次下载、安装。

## Linux项目部署

### **手工部署项目**

1. 在IDEA中开发SpringBoot项目并打包成jar包

2. 将jar包上传到Linux服务器

   ```
   mkdir /usr/local/app		创建目录,将项目jar包放到此目录
   ```

3. 启动SpringBoot程序

   ```
   java -jar [jar包]
   ```

4. 检查防火墙,确保8080端口对外开放,访问SpringBoot项目

5. 改为后台运行SpringBoot程序，并将日志输出到日志文件

   目前程序运行的问题

   - 线上程序不会采用控制台霸屏的形式运行程序，而是将程序在后台运行
   - 线上程序不会将日志输出到控制台，而是输出到日志文件，方便运维查阅信息

   ```
   nohup命令：英文全称 no hang up（不挂起），用于不挂断地运行指定命令，退出终端不会影响程序的运行
   语法格式：nohup Command [Arg…][&]
   参数说明：
   Command：要执行的命令
   Arg：一些参数，可以指定输出文件
   &：让命令在后台运行
   举例：
   nohup java -jar boot工程.jar &> hello.log &	后台运行java-jar命令，并将日志输出到hello.log文件
   ```

6. 停止SpringBoot程序

   ```
   ps -ef | grep java -jar
   kill -9 [进程号]
   ```

### **通过Shell脚本自动部署项目**

**操作步骤**

1. 在Linux中安装Git

   ```
   yum list git		列出git安装包
   yum install git		在线安装git
   ```

2. 使用Git克隆代码

   ```
   cd /usr/local/
   git clone https://gitee.com/fullofstar-p/reggie_take_out.git
   ```

3. 在Linux中安装maven

   ```
   tar -zxvf apache-maven-3.9.9-bin.tar.gz -C /usr/local
   vim /etc/profile									修改配置文件，加入如下内容
   export MAVEN_HOME=/usr/local/apache-maven-3.9.9
   export PATH=$JAVA_HOME/bin:$MAVEN_HOME/bin:$PATH
   source /etc/profile
   mvn -version
   vim /usr/local/apache-maven-3.9.9/conf/settings.xml		修改配置文件内容如下
   <localRepository>/usr/local/repo</localRepository>
   
   mkdir repo
   mkdir sh
   vim bootStart.sh
   ```

4. 编写Shell脚本(拉取代码、编译、打包、启动)

5. 为用户授予执行Shell脚本的权限

   ```
   chmod（英文全拼：change mode）命令是控制用户对文件的权限的命令
   Linux中的权限分为：读（r)、写（w)、执行（x）三种权限
   Linux的文件调用权限分为三级：文件所有者（Owner)、用户组（Group)、其它用户（Other Users)
   只有文件的所有者和超级用户可以修改文件或目录的权限
   要执行Shell脚本需要有对此脚本文件的执行权限，如果没有则不能执行
   ```

   | #    | 权限       | rwx  |
   | ---- | ---------- | ---- |
   | 7    | 读+写+执行 | rwx  |
   | 6    | 读+写      | rw-  |
   | 5    | 读+执行    | r-x  |
   | 4    | 只读       | r--  |
   | 3    | 写+执行    | -wx  |
   | 2    | 只写       | -w-  |
   | 1    | 只执行     | --x  |
   | 0    | 无         | ---  |

   举例:

   - chmod 777 bootStart.sh	为所有用户授予读、写、执行权限
   - chmod 755 bootStart.sh        为文件拥有者授予读、写、执行权限，同组用户和其他用户授予读、执行权限
   - chmod 210 bootStart.sh        为文件拥有者授予写权限，同组用户授予执行权限，其他用户没有任何权限

   注意:

   - 第1位表示文件拥有者的权限
   - 第2位表示同组用户的权限
   - 第3位表示其他用户的权限

6. 执行Shell脚本

7. 设置静态ip

   ```
   修改文件 /etc/sysconfig/network-scripts/ifcfg-ens33，内容如下：
   
   TYPE="Ethernet"
   PROXY_METHOD="none"
   BROWSER_ONLY="no"
   BOOTPROTO="static"					#使用静态IP地址，默认为dhcp
   IPADDR="192.168.138.128"			#设置的静态IP地址
   NETMASK="255.255.255.0"				#子网掩码
   GATEWAY="192.168.138.2"				#网关地址
   DNS1="192.168.138.2"				#DNS服务器
   DEFROUTE="yes"
   IPV4_FAILURE_FATAL="no"
   IPV6INIT="yes"
   IPV6_AUTOCONF="yes"
   IPV6_DEFROUTE="yes"
   IPV6_FAILURE_FATAL="no"
   IPV6_ADDR_GEN_MODE="stable-privacy"
   NAME="ens33"
   UUID="95b614cd-79b0-4755-b08d-99f1cca7271b"
   DEVICE="ens33"
   ONBOOT="yes"					#是否开机启用
   ```

