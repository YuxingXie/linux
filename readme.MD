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


### 1.3 软件安装


### 1.4 远程服务器

## 二：操作篇

### 2.1 本地部署一个java web应用程序

#### 2.1.1 安装java运行环境

#### 2.1.2 安装tomcat

#### 2.1.3 安装mysql

### 2.2 本地部署一个spring-boot应用程序

### 2.3 从GitHub克隆一个java项目并使用gradle构建jar

### 2.4 远程部署


## 三：工具篇

### 3.1 git

### 3.2 springboot CLI

### 3.3 gradle

### 3.4 maven

### 3.5 macOS brew install

作为开发人员最爱的操作系统，苹果macOS系统的brew工具我们也必须得学习以下。

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


