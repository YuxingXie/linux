# java程序员的linux

## 前言

 作为一名java程序员，Linux究竟要掌握到何种程度呢？这是这个项目需要探讨的问题。我将结合实际业务场景给出答案。当你在部署的时候出现了问题，到这里招解决方法可能会比翻Linux大头书更合适。
 
我不是写一本要出版的书，是写给自己以及某些Java程序员，部分部署工程师看的。我不会按章节顺序写，先给这个项目定一个大体章节，有心得就写进对应章节里。当然章节我可能也会调整，实现更合理的分门别类。
 
一些和Linux相关但不是Linux独有的东西我也放到这里研究，不再建立单独的研究项目了，比如git的研究就放到这个项目里。我觉得，只要能使用Linux Terminal实现功能的工具，
都可以放在这里研究。 

 
## 一 ：基础篇

### 1.1 Linux文件系统及权限

#### 1.1.1 Linux文件系统设计

#### 1.1.2 Linux文件基本操作

### 1.2 环境变量


### 1.3 网络配置

#### 1.3.1 ip地址设置

固定ip地址配置：

```text
cd /etc/sysconfig/network-scripts
ls -a
```
这时可以看到一些类似ifcfg-xxx之类的文件，xxx大概是网卡的名字，不知道可以用ip addr命令查找一下，我的是ens33，所以我要改的文件是ifcfg-ens33。

其中ifcfg-lo是使用主机模式时的配置吧(不太懂)，这个不是我们要改的。

```text
 vi ifcfg-ens33
```
要改这些地方：
```text
BOOTPROTO="static"
IPADDR="192.168.80.128"
NETMASK="255.255.255.0"
GATEWAY="192.168.80.1"
```
这样IP就固定了。

如果你的linux运行在VMWare这类虚拟机上，还要配置:

1. 编辑-->虚拟网络编辑器...
选中网卡后：
![](https://github.com/YuxingXie//linux/blob/master/assets/img/linux001.png)

2. NAT设置(s)...
![](https://github.com/YuxingXie/linux/blob/master/assets/img/linux002.png)


### 1.4 软件安装

#### 1.4.1 docker安装

#### 1.4.2 rabbitMQ安装

#### 1.4.3 gitLab安装



### 1.5 远程服务器

拷贝文件到远程服务器指定文件夹：
```text
scp local_file.jar user@ip/destdir
```



拷贝文件夹内的所有内容至服务器指定文件夹
```text
scp –r local_dir/* user@ip/destdir
```
### 1.5 其它

#### 1.5.1 修改系统时间

如果你的程序启动了定时器，但系统时间不对，那么客户端可能会认为程序是否会有问题。许多前端程序
可能会使用客户端时间。所以修改linux系统时间可能是需要掌握的。

linux有2套时间体系：系统时间和硬件时间。两个体系基本是独立运行的，据说也会自动同步，比如重启系统
会同步系统时间到硬件时间。

查看系统时间：
```text
date
```
修改系统时间
```text
date -s "2018-10-31 10:14:35"
```
同步系统时间到硬件时间(根据系统时间改写硬件时间)：
```text
hwclock --systohc
```
## 二：操作篇

### 2.1 本地部署一个java web应用程序

#### 2.1.1 安装java运行环境

#### 2.1.2 安装tomcat

#### 2.1.3 安装mysql

### 2.2 本地部署一个spring-boot应用程序

项目前端root路径:/home/admin/appData/zhnx_city_photo，程序启动后会自动生成这个目录，启动程序后把前端代码拷贝到这里.

项目上传路径：root:/home/admin/appData/zhnx_city_photo/upload：

小程序端记得改写API url后提交审核；

管理端无需修改了

可以先指定端口部署到服务器测试，无误后改回80端口

在本地打jar包运行测试是否有误

服务端记得改写profile,设置端口等

scp local_file.jar admin@10.96.51.81/opt/zhnx

如果permision denied,登录服务器，执行chomd 777 /opt/zhnx



进入目录后：java –jar xxxxx.jar

拷贝编译后的前端代码至服务器

创建的工作目录为/root/appData/zhnxCityPhoto/smswall
此目录需授权，切换到root用户：

su root

传输文件夹,注意用户是root否则永远permision denied：
scp –r local_dir root@10.96.51.81/root/appData/zhnxCityPhoto/smswall

浏览器输入网址404，猜想应该是admin启动程序权限不够不能访问静态文件夹造成的，切换到root启动程序
su root
java –jar xxx.jar

实际上并不是这个原因，而是拷贝的时候把静态文件的上层文件夹也拷贝过来了

正确的命令是：

scp –r local_dir/* root@10.96.51.81/root/appData/zhnxCityPhoto/smswall

成功！

### 2.3 从GitHub克隆一个java项目并使用gradle构建jar

### 2.4 远程部署


## 三：工具篇

### 3.1 git

### 3.2 springboot CLI

### 3.3 gradle

### 3.4 maven

### 3.5 macOS brew install


#### 3.5.1 安装brew:

```text
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" 
```
根据提示操作即可完成安装。

#### 3.5.2 brew安装maven

直接brew install maven会报/usr/local/share/man/man8没有权限。

```text
sudo chown -R xieyuxing /usr/local/share/man/man8

brew install maven


```
以下是mvn -v命令的打印：
```text
Apache Maven 3.5.4 (1edded0938998edf8bf061f1ceb3cfdeccf443fe; 2018-06-18T02:33:14+08:00)
Maven home: /usr/local/Cellar/maven/3.5.4/libexec
Java version: 1.8.0_131, vendor: Oracle Corporation, runtime: /Library/Java/JavaVirtualMachines/jdk1.8.0_131.jdk/Contents/Home/jre
Default locale: zh_CN, platform encoding: UTF-8
OS name: "mac os x", version: "10.14", arch: "x86_64", family: "mac"
```


