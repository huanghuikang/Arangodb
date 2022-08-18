# Arangodb
多模型数据库，值得一学
1、首先配置Arangodb环境，用Linux和Windows均可配置
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
  
2、创建document文档数据表：Disease、Drug、Disease_Drug（边界），将文件导入Arangodb数据库，界面只接受json文件，如文档是CSV,则需要将文档转换为json格式
3、创建edge文件数据图:Relation，将表的数据进行关联
