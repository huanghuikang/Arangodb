                                         Arangodb Learning
# Arangodb

Arangodb概念

ArangoDB是一款储存文档、图形并提供查询的多模型数据库,支持键值对、文档和图形模式的数据储存

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

ArangoDB查询语言(AQL)可用于检索和修改存储在ArangoDB中的数据。AQL主要是一种声明性语言，AQL类似于结构化查询语言(SQL)。AQL支持读取和修改集合数据，但不支持创建和删除数据库、集合和索引等数据定义操作。它是一种纯数据操作语言(DML)，而不是数据定义语言(DDL)或数据控制语言(DCL)。

Collection：集合由文档组成。它由其集合标识符唯一标识。它还有一个惟一的名称，客户端应该使用它来识别和访问它。集合可以重命名。这将更改集合名称，但不会更改集合标识符。集合的类型由用户在创建集合时指定。目前有两种类型:文档和边缘。默认为文档类型。

	Document：文档，可以储存一条记录
	
	Edge: 边缘，可以储存一条记录，与document不同，edge储存的是节点之间的关系（带有_from和_to）
	
View：视图由文档组成。它由其标识符唯一标识。它还有一个唯一的名称，客户端应该使用它来识别和访问它。视图可以重命名。这将更改视图名称，但不会更改视图标识符。视图具有由用户在创建视图时指定的类型。

当前唯一可用的视图类型是ArangoSearch。

Graph：图表，根据指定的一个或多个Document和Edge进行结合，组成一个Graph

-------------------------------------------

Arangodb基本使用

ArangoDB 的查询语言 AQL 检索我们的文档。

直接查看Collection目录里面有Dcument或Edge，点击其中一个文档，里面有相关文档的信息，可以对文档的信息进行修改、删除操作，对数据内容进行新增、修改、删除操作及添加索引等。

<img width="960" alt="4" src="https://user-images.githubusercontent.com/35037130/203300077-30dd2b9d-55ea-4110-a978-94ab73d8a4de.png">
<img width="960" alt="5" src="https://user-images.githubusercontent.com/35037130/203300136-99c277d1-7bdf-4720-83c2-3cc29f2b564f.png">

(1)查询


单击QUERIES菜单以调出查询编辑器并键入以下内容（调整文档 ID 以匹配你的文档），查询结果如图（可以JSON显示，也可Table格式显示，Table更直观）

return document("disease","disease/117312")       
单击Execute运行

<img width="1440" alt="6" src="https://user-images.githubusercontent.com/35037130/203302063-b884564b-da86-4f0b-ab6e-16ec3ee287f7.png">
<img width="1306" alt="7" src="https://user-images.githubusercontent.com/35037130/203302834-ecfed703-f68c-4360-88ed-e3148a1ea55b.png">

返回组合查询：
return document(["disease/117310","disease/117311","disease/117315"])       
单击Execute运行

 DOCUMENT()是一个函数，用于检索单个文档或您知道_keys 或_ids 的文档列表。这种类型的查询称为数据访问查询。不会创建、更改或删除任何数据。
 <img width="1315" alt="8" src="https://user-images.githubusercontent.com/35037130/203305002-d3a8df6c-1c26-4213-9215-b3fca129c709.png">
 
 代码查询全表数据：
 for c in disease
    return c
 <img width="1440" alt="8_1" src="https://user-images.githubusercontent.com/35037130/203536195-092ec77a-8d52-49cd-b8db-1cfbc15854d1.png">

(2)新增
在Collection目录中的Dcument点击新增
<img width="960" alt="9" src="https://user-images.githubusercontent.com/35037130/203532707-de1e3be8-f5e6-4d8c-b378-c65c9ef53a1d.png">

在QUERIES目录中录入INSERT代码新增
<img width="1440" alt="10" src="https://user-images.githubusercontent.com/35037130/203533164-c2da7f17-ab6b-4a39-8add-1f5cd7002c07.png">

还可通过Collection目录中的Dcument的导入新增
<img width="1440" alt="11" src="https://user-images.githubusercontent.com/35037130/203533686-cf4bf3d2-7998-433c-bb51-4e36f140cc6a.png">

（3）删除及修改
在Collection目录中的Dcument进行操作
<img width="1440" alt="12" src="https://user-images.githubusercontent.com/35037130/203535067-359b029a-3a21-4458-a675-18afbf4fcd3c.png">

在QUERIES代码修改：
update "117310" with{icd10: " slightly raised" } in disease
<img width="1440" alt="13" src="https://user-images.githubusercontent.com/35037130/203539395-42a9315d-2cd8-4dc4-9dd8-579b5e552ca0.png">

替换整个文档内容需要使用：
replace "117310" with {...} in disease

在QUERIES代码删除：
remove "117310" in disease
或 for c in disease remove c in disease 

下面将进一步学习
AQL条件查询：
filter关键字，过滤条件、返回固定列、别名

for c in disease 
filter c.ko=="H00835" or c.ko == "H01913"
filter c.icd10 != null
return {"名称":c.name,"描述" : c.description,"疾病类别":c.disease_category}
<img width="1440" alt="14" src="https://user-images.githubusercontent.com/35037130/203769465-b2e37dcc-680d-4daf-a701-10134e1380ad.png">

limit()：限制文档的数量
for c in disease limit(5) return c.name

for c in disease limit 4,6 return c.name    --跳过一定数量的记录并返回接下来的n 条文档

sort():对文档的进行排序,desc 升序   asc 升序，desc  降序
for c in disease 
sort c.name desc
limit 10
return c.name

多表查询：Characters 角色文档，Traits 角色特征文档
DOCUMENT(): 函数可用于通过文档标识符查找单个或多个文档

for c in Characters return c
for c in Traits return c

通过characters查询traits角色的属性
for c in Characters
    return document("Traits", c.traits)

合并查询角色属性
for c in Characters
    return merge(c, { traits: DOCUMENT("Traits", c.traits)[*].en } )
<img width="1440" alt="15" src="https://user-images.githubusercontent.com/35037130/203777401-59cb944a-2f01-42d2-9db9-32f07fe0931e.png">



-------------------------------------------
实战：

二、创建document文档数据表：Disease、Drug、Disease_Drug(边界)，将文件导入Arangodb数据库，界面只接受json文件，如文档是CSV,则需要将文档转换为json格式。

三、创建GRAPHS文件数据图,点击设置，将GRAPG Name、Edge definitions、fromCollections、toCollections、Vertex collections点保存即可创建图。
