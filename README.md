                                         Arangodb Learning
# Arangodb

多模型数据库，值得一学

一、首先配置Arangodb环境，用Linux和Windows均可配置
Linux的配置方法如下：

a、下载安装包：https://www.arangodb.com/download/

b、安装Arangodb：sudo yum install arangodb3-3.6.0-1.0.x86_64.rpm

c、设置root密码：运行arango-secure-installation

d、如需修改访问地址，则更新配置文件/etc/arangodb3/arangod.conf
	vim arangod.conf
	默认：endpoint = tcp://127.0.0.1:8529，默认端口为8529
	如：endpoint = tcp://10.10.10.1:8529
	
e、开启ArangoDB

	systemctl start arangodb3.service
	
	systemctl stop arangodb3.service       #关闭arangoDB
	
	systemctl restart arangodb3.service    #重启arangoDB
	
f、查看arangoDB运行状态

	systemctl status arangodb3.service ,出现active为正常运行
	
-----------------------------------------------------------------------------
window系统配置方法如下：

1、下载Arangodb压缩包：

链接：https://pan.baidu.com/s/117vOGh-HKKmIFwk7C1SAlQ 

提取码：as4w

2、Windows配置环境变量，将解压包的ArangoDB3e-3.7.18_win64\usr\bin配置到PATH系统变量中

3、双击打开bin文件夹中的arangodb.exe执行文件

4、打开浏览器进入http://127.0.0.1:8529/_db/_system/_admin/aardvark/index.html#login（若没修改arangod.conf配置文件，一般地址不变）

5、登录界面用root用户，密码为空
<img width="1440" alt="1" src="https://user-images.githubusercontent.com/35037130/202941495-0abe5883-d856-4dbd-9b47-12765a63c852.png">

<img width="1440" alt="2" src="https://user-images.githubusercontent.com/35037130/202941602-ba8bd711-fe34-4059-b697-f06f768c4101.png">
出现如下界面说明登录成功
<img width="1440" alt="3" src="https://user-images.githubusercontent.com/35037130/202941853-9885a4e9-6e27-458f-b594-fbd21dff6802.png">

----------------------------------------------------------
Arangodb概念

ArangoDB是一款储存文档、图形并提供查询的多模型数据库,支持键值对、文档和图形模式的数据储存

ArangoDB查询语言(AQL)可用于检索和修改存储在ArangoDB中的数据。AQL主要是一种声明性语言，AQL类似于结构化查询语言(SQL)。AQL支持读取和修改集合数据，但不支持创建和删除数据库、集合和索引等数据定义操作。它是一种纯数据操作语言(DML)，而不是数据定义语言(DDL)或数据控制语言(DCL)。

Collection：集合由文档组成。它由其集合标识符唯一标识。它还有一个惟一的名称，客户端应该使用它来识别和访问它。集合可以重命名。这将更改集合名称，但不会更改集合标识符。集合的类型由用户在创建集合时指定。目前有两种类型:文档和边缘。默认为文档类型。

	Document：文档，可以储存一条记录
	
	Edge: 边缘，可以储存一条记录，与document不同，edge储存的是节点之间的关系（带有_from和_to）
	
View：视图由文档组成。它由其标识符唯一标识。它还有一个唯一的名称，客户端应该使用它来识别和访问它。视图可以重命名。这将更改视图名称，但不会更改视图标识符。视图具有由用户在创建视图时指定的类型。

当前唯一可用的视图类型是ArangoSearch。

Graph：图表，根据指定的一个或多个Document和Edge进行结合，组成一个Graph

-------------------------------------------

Arangodb基本使用



实战：

二、创建document文档数据表：Disease、Drug、Disease_Drug(边界)，将文件导入Arangodb数据库，界面只接受json文件，如文档是CSV,则需要将文档转换为json格式。

三、创建GRAPHS文件数据图,点击设置，将GRAPG Name、Edge definitions、fromCollections、toCollections、Vertex collections点保存即可创建图。
