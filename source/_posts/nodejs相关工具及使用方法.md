title: Nodejs相关工具及使用方法
date: { { date } }
categories: nodejs
tags: [nodejs工具]
---

## 概述

本文记录nodejs学习过程中的相关知识（主要是一些坑，记录下来防止自己再次陷入，也给新加入nodejs学习的朋友提个醒）。包括：nodejs多个版本管理切换工具使用，主流框架express使用，MongoDB数据库的安装及使用。

## Nodejs多版本切换工具（nvmw）

相信接触过Nodejs的朋友，对Nodejs使用不同版本可能造成的不兼容问题非常头疼，由于本人没有研究过Linux系统，用的是windows系统（据说windows系统下nodejs坑特别多），首先就是网上各种找工具，windows下的工具能用貌似不多。要么不能用，要么收费，反正各种问题。最后找到了一款 `nvmw`,免费且在windows下使用很方便。

### 使用步骤

1. 下载 git clone https://github.com/hakobera/nvmw （没有用过github的朋友，请先了解下github）；
2. 设置环境变量：把nvmw的路径添加到系统环境变量（方便命令行直接操作nvmw）。添加步骤：右键我的电脑--属性--高级系统设置--环境变量--选中系统变量下Path行双击进入--新建--输入nvmw的路径如(D:/nvmw)；
3. 打开cmd，输入nvmw，会出现命令列表；

### 常用命令

+ `nvmw ls` #查看已安装的nodejs列表
+ `set "NVMW_NODEJS_ORG_MIRROR=https://npm.taobao.org/dist"` #设置nodejs资源下载地址（如果不设置，直接安装会报错）
+ `nvmw install v4.0.0` #安装nodejs 4.0.0版本（如果出现失败多试几次，我在安装的时候总是失败。自己手动在nvmw文件夹下新建nodejs相关版本文件夹，如v4.0.0文件夹，然后到http://nodejs.org/dist/ 下载对应版本的.exe文件到v4.0.0文件夹下）
+ `nvmw use v4.0.0` #切换到v4.0.0版本
+ `node -v` #查看当前使用的nodejs版本（显示v4.0.0）。

## Express安装及使用

### 安装

1. `npm install -g express@3` #安装3.x版本 若安装最新版去掉`@3`即可 `-g`全局安装 保证在计算机任何地方都可以直接使用express命令；（提示：如果想切换express版本，直接重新安装对应版本即可覆盖之前版本）
2. `npm install -g express-generator` #express 4.x以后将express命令独立到express-generator包中，所以想使用express初始化项目目录得先安装express-generator。

### 使用

+ `express -h` #查看帮助信息
+ `express -e` #使用ejs模板引擎（默认是jade模板）
+ `express myapp` #初始化项目（使用这个命令之前，先把命令行路径切换到指定位置，该命令会在当前位置创建一个myapp项目文件夹）

## MongoDB安装及使用

### 安装

1. 下载地址：http://www.mongodb.org/downloads
2. 解压缩到自己想要安装的目录，例如`D:\mongodb`
3. 创建文件夹`d:\mongodb\data\db`,`d:\mongodb\data\log`，分别用来安装存放db和日志文件
4. 开启`mongod.exe`程序 运行cmd 执行以下命令:(1)>`cd d:\mongodb\bin` (2)>`d:\mongodb\bin>mongod -dbpath "d:\mongod\data\db"`
5. 新开一个cmd窗口，进入mongodb/bin目录，输入`mongo`或`mongo.exe`，进入test这个数据库。显示如下信息则表明数据库开启成功。![alt 开启mongodb数据库](/uploads/images/mongodb_test.jpg)
6. 当`mongod.exe`被关闭时，`mongo.exe`就无法连接到数据库了，因此每次使用都要开启`mongod.exe`程序，比较麻烦。可以将MongoDB安装为windows服务。 以管理员运行cmd，进入`d:\mongodb\bin`目录，输入`mongod --dbpath "d:\mongodb\data\db" --logpath "d:\mongodb\data\log\MongoDB.log" --install --serviceName "MongoDB"`  再输入`net start MongoDB`启动MongoDB服务，将会显示：![alt 开启MongoDB服务成功](/uploads/images/mongodb_test2.jpg)
7. 关闭服务和删除进程  `net stop MongoDB` #关闭服务 `mongod --dbpath "d:\mongodb\data\db" --logpath "d:\mongodb\data\log\MongoDB.log" --remove --serviceName "MongoDB"`(注意这里不是install了) #删除进程

### 使用

> 常用命令

+ `show dbs` #显示数据库列表
+ `use dbname` #进入dbname数据库，没有也没关系（在数据库中创建集合后会自动创建数据库）
+ `show collections` #显示数据库中的集合，相当于表

> 创建和新增

+ `db.person.save({'name':'liuwei'})` #在数据库中创建了名为person集合，并新增一条数据{'name':'liuwei'}
+ `db.person.insert({'name':'fengge','age':'25'})` #person集合中新增一条数据
+ `save`和`insert`区别 当新插入的数据的主键(_id)已经存在，`save`会更新该条数据 `insert`则会报错 

> 删除

+ `db.person.remove({'name':'liuwei'})` #删除{'name':'liuwei'}这条数据
+ `db.person.remove({})` #删除person集合内所有数据
+ `db.peroson.drop()`或`db.runCommand({'drop':'person'})` #删除集合person
+ `db.runCommand({'dropDatabase':1})` #删除当前数据库

> 查找

+ `db.person.find()` #查找person集合中所有数据
+ `db.person.findOne()` #查找person集合中第一条数据

> 修改

+ `db.person.update({'age':'300'},{'name':'haha','age':'22'})` #修改含有{'age':'300'}的数据为{'name':'haha','age':'22'}主键后的所有数据都将被替换 第一个参数为查找条件，第二个参数为替换后的数据 主键不可替换 ![alt 修改数据](/uploads/images/mongodb_test3.jpg)


	