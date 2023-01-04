                                         Arangodb Learning
# Arangodb

ArangoDB conception

Arangodb概念

ArangoDB is a multi-model database that stores documents, graphs and provides queries. It supports data storage of key-value pairs, documents and graph modes.

ArangoDB 是一款储存文档、图形并提供查询的多模型数据库,支持键值对、文档和图形模式的数据储存。

ArangoDB is a multi-model, open-source database with flexible document, graph, and key-value data models. Build high-performance applications using a convenient SQL-like query language or JavaScript extensions.

ArangoDB 是一个多模型、开源数据库，具有灵活的文档、图形和键值数据模型。使用方便的类似 SQL 的查询语言或 JavaScript 扩展构建高性能应用程序。

Databases are sets of collections. Collections store records, which are referred to as documents.

数据库是集合的集合。 集合存储记录，称为文档。

First configure the Arangodb environment, both Linux and Windows can be configured.

一、首先配置Arangodb环境，用Linux和Windows均可配置。

The Linux configuration method is as follows:

Linux的配置方法如下：

Download the installation package: https://www.arangodb.com/download/

a、下载安装包：https://www.arangodb.com/download/

Install Arangodb: sudo yum install arangodb3-3.6.0-1.0.x86_64.rpm

b、安装Arangodb：sudo yum install arangodb3-3.6.0-1.0.x86_64.rpm

set root password and running : arango-secure-installation

c、设置root密码：运行arango-secure-installation

If you need to modify the access address, update the configuration file /etc/arangodb3/arangod.conf

	vim arangod.conf
	
	default: endpoint = tcp://127.0.0.1:8529 and the port is 8529
	
	for example: endpoint = tcp://10.10.10.1:8529
	
d、如需修改访问地址，则更新配置文件 /etc/arangodb3/arangod.conf

	vim arangod.conf
	
	默认：endpoint = tcp://127.0.0.1:8529，默认端口为8529
	
	如：endpoint = tcp://10.10.10.1:8529
	
then we running ArangoDB
	systemctl start arangodb3.service
	
	systemctl stop arangodb3.service
	
	systemctl restart arangodb3.service

e、开启ArangoDB

	systemctl start arangodb3.service
	
	systemctl stop arangodb3.service       #关闭arangoDB
	
	systemctl restart arangodb3.service    #重启arangoDB

View the running status of arangoDB
	systemctl status arangodb3.service

f、查看arangoDB运行状态

	systemctl status arangodb3.service ,出现active为正常运行
	
-----------------------------------------------------------------------------
The windows system configuration method is as follows:

windows系统配置方法如下：

Download the Arangodb compressed package : https://pan.baidu.com/s/117vOGh-HKKmIFwk7C1SAlQ   

passward: as4w

1、下载Arangodb压缩包：

链接：https://pan.baidu.com/s/117vOGh-HKKmIFwk7C1SAlQ 

提取码：as4w

Windows configuration environment variables, and unpack the ArangoDB3e-3.7.18_win64\usr\bin Configured in the PATH system variable.

2、Windows配置环境变量，将解压包的 ArangoDB3e-3.7.18_win64\usr\bin 配置到 PATH 系统变量中。

Double-click to open the arangodb.exe execution file in the bin folder.

3、双击打开bin文件夹中的 arangodb.exe 执行文件

then open the browser and enter http://127.0.0.1:8529/_db/_system/_admin/aardvark/index.html#login (if don't update arangod.conf, he general URL remains unchanged)

4、打开浏览器进入 http://127.0.0.1:8529/_db/_system/_admin/aardvark/index.html#login（若没修改 arangod.conf 配置文件，一般地址不变）

The login interface uses the root user, and the password is empty.

5、登录界面用root用户，密码为空.
<img width="1440" alt="1" src="https://user-images.githubusercontent.com/35037130/202941495-0abe5883-d856-4dbd-9b47-12765a63c852.png">

<img width="1440" alt="2" src="https://user-images.githubusercontent.com/35037130/202941602-ba8bd711-fe34-4059-b697-f06f768c4101.png">

The following interface appears to indicate that the login is successful.

出现如下界面说明登录成功。

<img width="1440" alt="3" src="https://user-images.githubusercontent.com/35037130/202941853-9885a4e9-6e27-458f-b594-fbd21dff6802.png">

----------------------------------------------------------

ArangoDB查询语言(AQL)可用于检索和修改存储在ArangoDB中的数据。AQL主要是一种声明性语言，AQL类似于结构化查询语言(SQL)。AQL支持读取和修改集合数据，但不支持创建和删除数据库、集合和索引等数据定义操作。它是一种纯数据操作语言(DML)，而不是数据定义语言(DDL)或数据控制语言(DCL)。

Collection：集合由文档组成。它由其集合标识符唯一标识。它还有一个惟一的名称，客户端应该使用它来识别和访问它。集合可以重命名。这将更改集合名称，但不会更改集合标识符。集合的类型由用户在创建集合时指定。目前有两种类型:文档和边缘。默认为文档类型。

	Document：包含文档，每个文档都是一个 JSON 对象；内置主索引，每个文档都有一个唯一的_key，可以快速查找；如果文档用作图中的节点，则文档可以是顶点。
	
	Edge: 包含文档，但具有特殊边属性 _from :源顶点的_id值， _to :目标顶点的_id值；每个边缘集合的内置边缘索引；存放关系的地方，类似于 SQL 数据库系统中的多对多关系（交叉表）。
	
View：视图由文档组成。它由其标识符唯一标识。它还有一个唯一的名称，客户端应该使用它来识别和访问它。视图可以重命名。这将更改视图名称，但不会更改视图标识符。视图具有由用户在创建视图时指定的类型。

当前唯一可用的视图类型是ArangoSearch。

Graph：图表，根据指定的一个或多个Document和Edge进行结合，组成一个Graph

-------------------------------------------

Arangodb基本使用

关键字：
<img width="364" alt="19" src="https://user-images.githubusercontent.com/35037130/204262888-11b6945b-f68f-4e36-81b7-2c142dbcac0f.png">

数字类型：

  空值：值 null 可用于表示空值或不存在的值，它不为0也不等于字符串 "" 。
  
  boolean 型：布乐数据类型有两种可能，true 和 false 。
  
  number 型：整数和实数（浮点数），可用 + 或 - 标记。
  
  string 型：必须用单引号或双引号括起，使用特殊字符时，需要用反斜杠 \ 转意。（所有字符串都必须采用 UTF-8 编码）
  
  复合类型：数组
    array:末命名值的组合，每个值都可以通过它们的位置访问，称为列表。
      数组/列表：数组以中括号 [ 数组值 ] ，数组值用逗号分隔。
      
    object:命名值的组合，每个值都可以通过它们的名称访问，文档是顶层的对象。
       文档/文件：对象声明用大括号 ｛ 对象/值对 ｝ ，对象中的每个属性是一个名称/值对。属性名称和值使用冒号分隔 : 。名称是字符串，可以带引号或不带引号，而值可以是任何类型，包括子对象。特殊字符需要转意。
   
   绑定参数：

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

UPDATE 允许部分编辑现有文档, 关键字后跟文档键（或具有属性的文档/对象 ） _key 以标识要修改的内容。要更新的属性写为 WITH 关键字后的对象。 IN 表示在哪个集合中执行此操作，就像 INTO （这两个关键字在这里实际上可以互换）

REPLACE，它会删除所有属性（除了 _key 和 _id，它们保持不变）并且只添加指定的属性。

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

sort():对文档的进行排序, DESC 降序， ASC 可以用于升序。 ASC 虽然是默认值，但可以省略。  多列排序按照从上到下，从左往右排序。
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

-----------------------
遍历解释：遍历意味着以特定方式沿着图形的边缘行走，可选择使用一些过滤器。遍历在图形数据库中非常有效。在 ArangoDB 中，这是通过您已经听说过的混合索引类型实现的：边缘索引。

图遍历语法：
FOR vertex[, edge[, path] IN [min[..max] OUTBOUND|INBOUND|ANY startVertex edgeCollection[, more…]

FOR 发出最多三个变量
	vertex (object):遍历中的当前顶点。
	edge (object, optional)：遍历中的当前边
	path (object, optional)：具有两个成员的当前路径的表示
		vertices：此路径上所有顶点的数组
		edges：此路径上所有边的数组

IN min..max ：定义遍历的最小和最大深度。如果不指定，min默认为1，max默认为min。
![22](https://user-images.githubusercontent.com/35037130/204992116-7fdab22b-3134-4c16-b238-fbdcc6f3348a.png)

** OUTBOUND/INBOUND/ANY ：定义搜索的方向。

![21](https://user-images.githubusercontent.com/35037130/204991692-9f7bff0f-4238-497c-a3ed-39107695284e.png)

例如：
返回可以从洛杉矶国际机场 (LAX) 沿着航班边缘直接到达（第一步）的所有机场的名称

WITH airports 
FOR airport IN 1..1 OUTBOUND 'airports/LAX' flights
RETURN DISTINCT airport.name

WITH:AQL 查询可以以 WITH 关键字开头，后跟查询隐式读取的集合列表。在集群环境中进行图形遍历时，这是必需的。通过隐式，意思是集合没有像前面的例子那样在语言结构中明确指定。

这里确实明确声明了航班集合，但我们实际上并没有在 FOR 声明中声明机场，这就是它作为 WITH 语句的一部分包含在内的原因。这样做可以确保查询优化器可以在集群环境中保持运行时的性能。
AQL 查询解析器会自动检测在查询中明确使用的集合。查询中涉及但查询解析器无法自动检测到的任何其他集合都可以使用 WITH 语句手动指定。

--------------------------------

Graph: 图形遍历，两个文档之间的关系可以搭建一个图形。在ArangoDB中，两个文档通过边Edge的边缘文档链接。Edge文档存储在边缘集合中，通过 _from 和 _to 两个属性作为边缘条件。

创建disease（疾病），drug（药物）和gene_tmp(pathogen_disease,病原体)三个文档及一个dd_edge边缘文档，此边缘文档联合疾病和药物。（文档的创建和数据导入不做赘述）

最后在Graph目录新建Graph,填写对应 _from 和 _to 的关系，如下图

<img width="486" alt="16" src="https://user-images.githubusercontent.com/35037130/203978090-fc96ada3-96b6-474e-9a71-0f14b5ebb852.png">

<img width="1440" alt="18" src="https://user-images.githubusercontent.com/35037130/203978344-a56076d1-0704-4cb8-8d04-3f1adbd44bdc.png">

-------------------------------------------------------
遍历选项：

有关遍历的文档可看到还有控制遍历行为的选项（OPTIONS）。对于最小深度大于或等于 2 的遍历，有两种遍历图形的选择：

	Depth-first 深度优先（默认）：继续沿着该路径上的起始顶点到最后一个顶点的边或直到达到最大遍历深度，然后沿着其他路径走。
	
	Breadth-first 广度优先（可选）：跟随从起始顶点到下一层的所有边，然后跟随它们邻居的所有边到另一层并继续这种模式，直到没有更多的边可以跟随或达到最大遍历深度。

![23](https://user-images.githubusercontent.com/35037130/205030816-ad5b8a94-4bf4-4cfc-9472-f31d025fe88d.png)
![24](https://user-images.githubusercontent.com/35037130/205030859-7d9387eb-f28b-428b-81a6-03db6f139451.png)

**单个顶点的边没有特定的顺序。因此，S→C 可以在 S→A 和 S→B 之前返回。仍然使用广度优先搜索在较长路径之前返回较短的路径。

遍历唯一性：并非每个图都只有一条从所选起始顶点到其连接顶点的路径。

默认情况下，如果再次遇到已经访问过的边，则沿任何路径的遍历都会停止。它可以防止您的遍历在达到最大遍历深度之前绕圈子运行。不产生过多不需要的路径是一种安全措施。除非以其他方式配置遍历，否则路径上的重复顶点是允许的。

*** 为了阻止起始顶点（或其他顶点）被多次访问，我们可以通过两种方式为顶点启用唯一性（ OPTION{ bfs: true }（广度优先搜索））：

	uniqueVertices: 'path' 确保每个单独的路径上没有重复的顶点。
	
	uniqueVertices: 'global' 确保在整个遍历过程中访问每个可到达的顶点一次。
	
	uniqueVertices: 'global'有去重的作用，与DISTINCT比较，RETURN DISTINCT仅在遍历返回所有顶点（巨大的中间结果）后才对机场进行重复数据删除，而 uniqueVertices: 'global' 是一个遍历选项，指示遍历器立即忽略重复项。

最短路径查询：
WITH airports FOR v IN OUTBOUND SHORTEST_PATH 'airports/BIS' TO 'airports/JFK' flights
 RETURN v.name
 
Shortest_Path 查询可以返回不同的结果。它只是找到并返回可能的多个最短路径之一。



--------------------

函数：

CONCAT() ：是一个可以将元素连接成字符串的函数。
for c in Characters
return concat(c.name,"'s age is",c.age)
<img width="1440" alt="20" src="https://user-images.githubusercontent.com/35037130/204960111-662d1e8b-fa7d-4ee6-a473-0f1798db636a.png">

LENGTH() ：获取数组的长度或文档中的属性数。

COLLECT对中间结果进行无条件分组，也就是将所有过滤后的文档分组到一起。

-------------------------------------------
实例一：

添加文档集合：Characters 

AQL语句：INSERT document INTO collectionName

文档是一个对象，就像您从 JavaScript 或 JSON 中了解到的那样，它由属性键和值对组成。键总是字符序列（字符串），而属性值可以有不同的类型：null、boolean (true, false)、number (integer and floating point)、string、array、object

接入文档：
INSERT {
  "name": "Ned",
  "surname": "Stark",
  "alive": true,
  "age": 41,
  "traits": ["A","H","C","N","P"]
} INTO Characters

或

LET data = [
  { "name": "Robert", "surname": "Baratheon", "alive": false, "traits": ["A","H","C"] },
  { "name": "Jaime", "surname": "Lannister", "alive": true, "age": 36, "traits": ["A","F","B"] },
  ...
  { "name": "Roose", "surname": "Bolton", "alive": true, "traits": ["H","E","F","A"] },
  { "name": "The High Sparrow", "alive": true, "traits": ["H","M","F","O"] }
]

FOR d IN data
  INSERT d INTO Characters

用关键字 LET 定义一个变量，然后用 FOR 迭代 INSERT 文档 Characters 中

阅读文件AQL语法：FOR variableName IN collectionName 或 DOCUMENT() 函数 

FOR c IN Characters RETURN c

RETURN DOCUMENT("Characters/85502")  或  RETURN DOCUMENT("Characters", [ "85502","85503" ])

修改文件AQL语法：UPDATE documentKey WITH object IN collectionName  或  REPLACE documentKey WITH object IN collectionName

删除文件AQL语法：REMOVE documentKey IN collectionName

带 FOR 迭代查询：

FOR c IN Characters FILTER c._key == "85502" RETURN c  或 FOR c IN Characters FILTER c._key in ( "85502" , "85503") RETURN c

运算符： == 、 != 、 >= 、 <= 、 > 、< 、and --> &&（连词） 、or --> ||(析取) 、not --> !（否定/反转） 、 in 、not in 、 like

合并字符和特征：字母——特征键——解析为有意义的特征，需要合并字符文档和特征文档中的数据，可以通过使用MERGE()函数和子查询来实现。
FOR c IN Characters
  RETURN MERGE(c, 
		  {
		    traits: (
		      FOR key IN c.traits
			FOR t IN Traits
			  FILTER t._key == key
			  RETURN t.en
			    )
		  }
              )
	      
<img width="1440" alt="25" src="https://user-images.githubusercontent.com/35037130/205229886-34a80ee6-63a7-41bb-b707-1fd692280d4e.png">

图遍历,确定关系

创建边缘 Edge

LET data = [
    {
        "parent": { "name": "Ned", "surname": "Stark" },
        "child": { "name": "Robb", "surname": "Stark" }
    }, 
    ... 
    , {
        "parent": { "name": "Jaime", "surname": "Lannister" },
        "child": { "name": "Joffrey", "surname": "Baratheon" }
    }
]

FOR rel in data
    LET parentId = FIRST(
        FOR c IN Characters
            FILTER c.name == rel.parent.name
            FILTER c.surname == rel.parent.surname
            LIMIT 1
            RETURN c._id
    )
    LET childId = FIRST(
        FOR c IN Characters
            FILTER c.name == rel.child.name
            FILTER c.surname == rel.child.surname
            LIMIT 1
            RETURN c._id
    )
    FILTER parentId != null AND childId != null
    INSERT { _from: childId, _to: parentId } INTO ChildOf
    RETURN NEW

--------------------
实战：

二、创建document文档数据表：Disease、Drug、Disease_Drug(边界)，将文件导入Arangodb数据库，界面只接受json文件，如文档是CSV,则需要将文档转换为json格式。

三、创建GRAPHS文件数据图,点击设置，将GRAPG Name、Edge definitions、fromCollections、toCollections、Vertex collections点保存即可创建图。
