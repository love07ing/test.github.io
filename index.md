
Mysql 查询优化建议

 

 

了解Mysql查询过程

1、客户端与服务器建立TCP连接，客户端发送查询语句给到Mysql服务器

2、Mysql服务器先检查Query Cache，如果命中缓存则返回缓存结果，否则进入下一步解析

3、解析器针对SQL语句做语法解析，生成解析树；预处理器进一步检查，生成新解析树

4、优化器根据新解析树生成执行计划

5、执行器调用存储引擎API接口获取数据

6、Mysql服务器缓存查询结果，返回结果给到客户端。

7、关闭连接，释放连接线程。

查询过程图一：

 


 

 

查询过程图二：

 


 

 

 

优化建议

1、状态监控和检测

show status

 

show processlist

 

 

 

2、开启慢查询日志

在配置文件 my.cnf 中的 [mysqld] 一行下边添加两个参数：

slow_query_log = 1

slow_query_log_file=/var/lib/mysql/slow-query.log

long_query_time = 2

log_queries_not_using_indexes = 1

 

 

 

 

3、分析SQL执行计划

 

explain select * from category;

 

附表

DDL/DML/DCL区别概述

https://share.weiyun.com/5VApXpb
