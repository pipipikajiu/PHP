## 1　关系型数据库
- 1 .关系型数据库管理系统（RDBMS）具有以下特点：
    能够实现一种具有表、列与索引的数据库。
    保证不同表的行之间的引用完整性。
    能自动更新索引。
    能解释 SQL 查询，组合多张表的信息。
    
    
## 2 Mysql
   - 1 . mysql  数据类型:
        - 1.1 . 数值数据类型:
            - 1.1.1 . 整数类型
                - [1] . int
                - [2] . tinyint
                - [3] . smallint
                - [4] . mediumint
                - [5] . bigint
            - 1.1.2 . 浮点小数类型
                - [1] . float
                - [2] . double
            - 1.1.3 . 定点小数类型
                - [1] . 小数类型
        - 1.2 . 时间/日期类型
            - 1.2.1 . year
            - 1.2.2 . time
            - 1.2.3 . date
            - 1.2.4 . datetime
            - 1.2.5 . timestamp
        - 1.3 . 字符串类型
            - 1.3.1 . 文本字符串
                - [1] . char
                - [2] . varchar
                - [3] . tinytext
                - [4] . text
                - [5] . mediumtext
                - [6] . longtext
                - [7] . enum
                - [8] . set
            - 1.3.2 . 二进制字符串
                - [1] . (bit,binary,varbinary,tinyblob,blog,mediumblob,longblobi)
## 3 列类型优化:
```javascript
       字段类型优先级: 整形>date,time>enum,char>varchar>blob,text
       整型:定长,没有国家地区之分,没有字符集的差异,
       字符串类型,在排序时 要考虑字符集与校对集 (排序规则),时间会稍微长点.
       time:定长,运算快,节省空间, 要考虑时区,写sql不方便.
       enum: 
       char:定长,考虑字符集和(排序)校对集,
       varchar:不定长 ,考虑字符集和(排序)校对集,
       text/blob:无法使用内存临时表,排序时只能在磁盘上进行.
```

## 4 . mysql数据类型:
```javascript
    1、整型
    MySQL数据类型	含义（有符号）
    tinyint(m)	1个字节  范围(-128~127)
    smallint(m)	2个字节  范围(-32768~32767)
    mediumint(m)	3个字节  范围(-8388608~8388607)
    int(m)	4个字节  范围(-2147483648~2147483647)
    bigint(m)	8个字节  范围(+-9.22*10的18次方)
    取值范围如果加了unsigned，则最大值翻倍，如tinyint unsigned的取值范围为(0~255)。


    int(m)里的m是表示SELECT查询结果集中的显示宽度，不知道这个m有什么用。
    int 占10位，存不了手机号（11位）

    2、浮点型(float和double):浮点型在数据库中存放的是近似值
    MySQL数据类型含义
    float(m,d)	单精度浮点型     8位精度(4字节)     m总个数，d小数位
    double(m,d)	双精度浮点型    16位精度(8字节)    m总个数，d小数位

    设一个字段定义为float(5,3)，如果插入一个数123.45678,实际数据库里存的是123.457，但总个数还以实际为准，即6位。

    3、定点数    定点类型在数据库中存放的是精确值

    浮点型在数据库中存放的是近似值，而定点类型在数据库中存放的是精确值。

    decimal(m,d) 参数m<65 是总个数，d<30且 d<m 是小数位。

    

    4、字符串(char,varchar,_text)

    MySQL数据类型	含义
    char(n)	固定长度，最多255个字符
    varchar(n)	可变长度，最多65535个字节
    tinytext	可变长度，最多255个字符
    text	可变长度，最多65535个字符
    mediumtext	可变长度，最多2的24次方-1个字符
    longtext	可变长度，最多2的32次方-1个字符
```
     

 ## 5 . mysql优化
 ```php
数据库优化的目的 :
 避免出现页面访问错误
  . 由于数据库链接timeout 产生页面 5xx错误
  . 由于慢查询造成页面无法加载
  . 由于阻塞造成数据无法提交  

 - 5.1 sql及索引
 - 5.1.1 . 结构良好的sql

 - 5.1.2 .根据sql建立有效的索引 

 - 5.1.3  . mysql慢查询日志
查看是否开启慢查询日志 show variables like 'slow_query_log'
设置没有索引的记录到慢查询日志 set global log_queries_not_using_indexes=on
查看超过多长时间的sql进行记录到慢查询日志 show variables like 'long_query_time'
设置慢查询的时间 set long_query_time=1

慢查日志中; Rows_sent:(): 发送行数;Rows_examined:():扫描行数
慢查日志分析工具 : pt-query-digest 慢查询日志路径

如何通过慢查日志发现有问题sql:
1 . 查询次数多且每次查询占用时间长的sql;
2 . I/O大的sql
    注意pt-query-digest 分析中的Rows examined项 越多证明I/O越大
3 . 为命中索引的sql
    Rows_sent:()和Rows_examined:()的对比


 - 5.2 数据表结构
范式 减少冗余 有利于sql的编写

 - 5.3 系统的配置
 打开文件数有限制
 mysql 是基于文件的 没打开一个表 就得打开文件
 - 5.4 硬件   
 ```


 mysql视图
 是一个虚拟表,用于存储查询语句, 第二次直接查询视图就可以. 存储与数据库中
 创建方式 : CREATE VIEW 视图明 sql语句
 查询视图 : select *from 视图明
 视图查询也可加过滤条件 select * from 视图名 where name='abc';
 查看当前库下所有视图 : show full tables where table_type like 'VIEW';
 删除视图 : drop view if exists 视图名.
