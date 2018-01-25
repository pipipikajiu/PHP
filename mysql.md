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
            - 1.1.3 . 浮点小数类型
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
     