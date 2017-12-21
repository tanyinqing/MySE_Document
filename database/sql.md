
- 一共有5中sql语言
- [数据控制语言](#20171219_1)

# Chapter 3 SQL 语言

## 基础语法

```sql
-- a SQL statement
SELECT * FROM table_name;
```

1. SQL 关键字不区分大小写  结构化查询语言 第四代语言
2. 分号 `;` 是区分语句的标志 命令式语言
3. MySQL 注释 单行注释和多行注释

  ```sql
  SELECT 1+1;     # This comment continues to the end of line
  SELECT 1+1;     -- This comment continues to the end of line
  SELECT 1 /* this is an in-line comment */ + 1;
  SELECT 1+
  /*
  this is a
  multiple-line comment
  */
  1;
  ```
4. 推荐使用完全限定表名  

5. 常用的 SQL 语句
  
  ```sql
  SELECT - extracts data from a database  
  UPDATE - updates data in a database
  DELETE - deletes data from a database
  INSERT INTO - inserts new data into a database
  CREATE DATABASE - creates a new database
  ALTER DATABASE - modifies a database
  DROP DATABASE - deletes a database
  CREATE TABLE - creates a new table
  ALTER TABLE - modifies a table
  DROP TABLE - deletes a table
  CREATE INDEX - creates an index (search key) 创建索引
  DROP INDEX - deletes an index
  ```

## SQL 语句
### 1. DDL

> Data Definition Language 数据定义语言

- SQL Create DB

  ```sql
  CREATE DATABASE database_name;
  ```

- SQL 数据类型  不同数据库数据类型不同
 
  > text, number, and Date/Time  字符和数字和日期

  1. Text types
<table>
    <tr>
      <th>Data type</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>CHAR(size)长度固定的，最大255</td>
      <td>Holds a fixed length string (can contain letters, numbers, and special 
	  characters). The fixed size is specified in parenthesis. Can store up to 
	  255 characters</td>
    </tr>
    <tr>
      <td><b>VARCHAR(size) 可变长度字符类型</b></td>
      <td>Holds a variable length string (can contain letters, numbers, and 
	  special characters). The maximum size is specified in parenthesis. Can 
	  store up to 255 characters. <b>Note:</b> If you put a greater value than 
	  255 it will be converted to a TEXT type</td>
    </tr>
    <tr>
      <td>TINYTEXT</td>
      <td>Holds a string with a maximum length of 255 characters</td>
    </tr>
    <tr>
      <td>TEXT 文本</td>
      <td>Holds a string with a maximum length of 65,535 characters</td>
    </tr>
    <tr>
      <td>BLOB 大的2进制数据</td>
      <td>For BLOBs (Binary Large OBjects). Holds up to 65,535 bytes of data</td>
    </tr>
    <tr>
      <td>MEDIUMTEXT 中文本</td>
      <td>Holds a string with a maximum length of 16,777,215 characters</td>
    </tr>
    <tr>
      <td>MEDIUMBLOB 音频</td>
      <td>For BLOBs (Binary Large OBjects). Holds up to 16,777,215 bytes of data</td>
    </tr>
    <tr>
      <td>LONGTEXT 特别长的文本</td>
      <td>Holds a string with a maximum length of 4,294,967,295 characters</td>
    </tr>
    <tr>
      <td>LONGBLOB 4个G</td>
      <td>For BLOBs (Binary Large OBjects). Holds up to 4,294,967,295 bytes of 
	  data</td>
    </tr>
    <tr>
      <td>ENUM(x,y,z,etc.)</td>
      <td>Let you enter a list of possible values. You can list up to 65535 
	  values in an ENUM list. If a value is inserted that is not in the list, a 
	  blank value will be inserted.<p><b>
		Note:</b> The values are sorted in the order you enter them.</p>
		<p>You enter the possible values in this format: ENUM('X','Y','Z')</td>
    </tr>
	<tr>
      <td>SET</td>
      <td>Similar to ENUM except that SET may contain up to 64 list items and 
	  can store more than one choice</td>
    </tr>
</table>

  2. Number types 数值类型
<table>
    <tr>
      <th style="width:20%">Data type 宽度安照比例</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>TINYINT(size)</td>
      <td>-128 to 127 normal. 0 to 255 UNSIGNED*. The maximum number of digits 
	  may be specified in parenthesis</td>
    </tr>
    <tr>
      <td>SMALLINT(size)</td>
      <td>-32768 to 32767 normal. 0 to 65535 UNSIGNED*. The maximum number of 
	  digits may be specified in parenthesis</td>
    </tr>
    <tr>
      <td>MEDIUMINT(size)</td>
      <td>-8388608 to 8388607 normal. 0 to 16777215 UNSIGNED*. The maximum 
	  number of digits may be specified in parenthesis</td>
    </tr>
    <tr>
      <td><b>INT(size) 最常用</b></td>
      <td>-2147483648 to 2147483647 normal. 0 to 4294967295 UNSIGNED*. The 
	  maximum number of digits may be specified in parenthesis</td>
    </tr>
    <tr>
      <td>BIGINT(size) 长整形</td>
      <td>-9223372036854775808 to 9223372036854775807 normal. 0 to 
	  18446744073709551615 UNSIGNED*. The maximum number of digits may be 
	  specified in parenthesis</td>
    </tr>
    <tr>
      <td>FLOAT(size,d) 单精度</td>
      <td>A small number with a floating decimal point. The maximum number of 
	  digits may be specified in the size parameter. The maximum number of 
	  digits to the right of the decimal point is specified in the d parameter</td>
    </tr>
    <tr>
      <td><b>DOUBLE(size,d) 双精度</b></td>
      <td>A large number with a floating decimal point. The maximum number of 
	  digits may be specified in the size parameter. The maximum number of 
	  digits to the right of the decimal point is specified in the d parameter</td>
    </tr>
    <tr>
      <td><b>DECIMAL(size,d) 跟钱有关的用</b></td>
      <td>A DOUBLE stored as a string , allowing for a fixed decimal point. The 
	  maximum number of digits may be specified in the size parameter. The 
	  maximum number of digits to the right of the decimal point is specified in 
	  the d parameter</td>
    </tr>
</table>

    > `INT(size)`
    
    > The size is just the display width, that is used when the field has ZEROFILL specified. 
 
  3. Date types 日期有关的
<table>
    <tr>
      <th>Data type</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><b>DATE</b></td>
      <td>A date. Format: YYYY-MM-DD<p><b>Note:</b> The supported range is from 
	  '1000-01-01' to '9999-12-31'</p></td>
    </tr>
    <tr>
      <td><b>DATETIME 年月日</b></td>
      <td>*A date and time combination. Format: YYYY-MM-DD HH:MI:SS<p><b>Note:</b> 
	  The supported range is from '1000-01-01 00:00:00' to '9999-12-31 23:59:59'</p></td>
    </tr>
    <tr>
      <td>TIMESTAMP</td>
      <td>*A timestamp. TIMESTAMP values are stored as the number of seconds 
	  since the Unix epoch ('1970-01-01 00:00:00' UTC). Format: YYYY-MM-DD 
	  HH:MI:SS<p><b>Note:</b> The supported range is from '1970-01-01 00:00:01' 
	  UTC to '2038-01-09 03:14:07' UTC</p></td>
    </tr>
    <tr>
      <td>TIME 时分秒</td>
      <td>A time. Format: HH:MI:SS<p><b>Note:</b> The supported range is from 
	  '-838:59:59' to '838:59:59'</p></td>
    </tr>
    <tr>
      <td>YEAR</td>
      <td>A year in two-digit or four-digit format.<p>
		<b>Note:</b> Values allowed in four-digit format: 1901 to 2155. Values 
		allowed in two-digit format: 70 to 69, representing years from 1970 to 
		2069</p></td>
    </tr>
</table>


- SQL Create Table

  ```sql
  CREATE TABLE table_name (
    column_name1 data_type(size),
    column_name2 data_type(size),
    column_name3 data_type(size),
    ....
  );
```

- SQL Drop 删除

  ```sql
  -- Drop database
  DROP DATABASE database_name;
  -- Drop table
  DROP TABLE table_name;
  -- Drop index in MySQL
  ALTER TABLE table_name DROP INDEX index_name;
  -- Truncate table  
  TRUNCATE TABLE table_name;
  ```

- SQL Constraints  字段进行限制
  1. 约束创建时间
    - 建表时创建
    
      ```sql
      CREATE TABLE table_name (
        column_name1 data_type(size) constraint_name,
        column_name2 data_type(size) constraint_name,
        column_name3 data_type(size) constraint_name,
        ....
      );
      ```
      
    - 建表后追加 `todo`
  - 非空约束 `Not Null`   不可以为空值
  
    ```sql
    CREATE TABLE PersonsNotNull (
      P_Id int NOT NULL,
      LastName varchar(255) NOT NULL,
      FirstName varchar(255),
      Address varchar(255),
      City varchar(255)
    );
    ```
  
  - 唯一约束 `Unique`  可以为空 不能重复 值唯一
  
    ```sql
    CREATE TABLE Persons (
      P_Id int NOT NULL,
      LastName varchar(255) NOT NULL,
      FirstName varchar(255),
      Address varchar(255),
      City varchar(255),
      CONSTRAINT uc_PersonID UNIQUE (P_Id,LastName) -- 另一种声明值唯一的方式
    );
    ```
  
  - 主键约束 `Primary Key`  不可以为空 值唯一 自增长

    ```sql
    -- 一般情况下的主键定义方式
    CREATE TABLE table_name (
      id INT AUTO_INCREMENT PRIMARY KEY,
      ...
    );
    ```
另一种声明方式
    ```sql
    CREATE TABLE Persons (
      P_Id int NOT NULL,
      LastName varchar(255) NOT NULL,
      FirstName varchar(255),
      Address varchar(255),
      City varchar(255),
      PRIMARY KEY (P_Id)
    );
    ```

  - SQL Foreign Key 建立表关联
    - 主表 父表（主键所在的表）部门表
    - 从表 子表（外键所在的表） 员工表
    - 必须引用主表主键
    - 外键和主键数据类型一致
    
    > [mySQL RESTRICT and NO ACTION MySQL限制和不动作](http://stackoverflow.com/a/5810024/3414180)
      
    ```
    -- 建立外键约束 和 4个引用的选项  即外键在删除和修改时执行的操作 这里写的比较麻烦，可以看例子
    [CONSTRAINT [symbol]] FOREIGN KEY
        [index_name] (index_col_name, ...)
        REFERENCES tbl_name (index_col_name,...)
        [ON DELETE reference_option] 引用选项
        [ON UPDATE reference_option]

    reference_option:
        RESTRICT | CASCADE | SET NULL | NO ACTION
    ```
    
    > temporarily disable a foreign key constraint in MySQL   在MySQL中暂时禁用外键约束

    ```sql
    -- Try DISABLE KEYS: 原来的外键都暂时失效了

    SET FOREIGN_KEY_CHECKS=0;

    -- make sure to 使外键重新生效

    SET FOREIGN_KEY_CHECKS=1;

    -- after.
    ```

  - 缺省值 `Default`
  
    ```sql
    CREATE TABLE Persons (
      P_Id int NOT NULL,
      LastName varchar(255) NOT NULL,
      FirstName varchar(255),
      Address varchar(255),
      City varchar(255) DEFAULT 'Sandnes' -- 使列在未定义的情况下生成默认值
    )
    ```

  - ~~SQL Check~~ `MySQL` 检查也就是在值插入时对值进行检查  mysql中不起作用
  
    >  The CHECK clause is parsed but ignored by all storage engines. 检查子句被解析，但被所有存储引擎忽略

    > [CHECK constraint in MySQL is not working MySQL中的检查约束不起作用](http://stackoverflow.com/questions/2115497/check-constraint-in-mysql-is-not-working)
  
- Auto Increment  自定增长

  ```sql
  CREATE TABLE Persons (
  ID int NOT NULL UNSIGNED AUTO_INCREMENT,
  ...
  PRIMARY KEY (ID)
  );
  ```

  ```sql
  ALTER TABLE Persons AUTO_INCREMENT = 100; -- 让主键的值从指定的值开始
  ```

- Alter  

  ```sql
  ALTER TABLE old_table_name RENAME new_table_name;-- 修改表的名字
  ```

  ```sql
  ALTER TABLE table_name
  ADD COLUMN column_name datatype [AFTER column_name | FIRST];

    -- 为表添加一列  指定列的位置
    ALTER TABLE db_day03.student ADD COLUMN marride INT(1) NOT NULL AFTER gender;
  ```

  ```sql
  ALTER TABLE table_name
  DROP COLUMN column_name;  -- 删除一列
  ```

  ```sql
  ALTER TABLE table_name
  MODIFY COLUMN column_name datatype [AFTER column_name | FIRST]; -- 修改列名
  ```
  
  ```sql
  ALTER TABLE table_name 
  ADD CONSTRAINT primary_key_name PRIMARY KEY(columns);-- 添加主键
  ```
  
  ```sql
  ALTER TABLE table_name
  CHANGE old_column_name new_column_name datatype [AFTER column_name | FIRST];  -- 修改列的名字
  ```
  - 为表追加外键 不推荐
  ```sql
  ALTER TABLE table_name
  ADD CONSTRAINT
  foreign_key_name
  FOREIGN KEY (columns)
  REFERENCES parent_table(columns)
  ON DELETE action
  ON UPDATE action;
  ```
  - 为表删除外键约束
  ```sql
  ALTER TABLE table_name 
  DROP FOREIGN KEY constraint_name;
  ```
  
  ```sql
  ALTER TABLE table_name DROP INDEX unique_column_name;
  ```
  
  ```sql
  -- Delete all duplicated rows except one
  ALTER IGNORE TABLE table_name
  ADD UNIQUE INDEX idx_name (column);

  -- If you want to keep the row with the lowest id value:
  DELETE n1 FROM names n1, names n2 WHERE n1.id > n2.id AND n1.name = n2.name;
  -- If you want to keep the row with the highest id value:
  DELETE n1 FROM names n1, names n2 WHERE n1.id < n2.id AND n1.name = n2.name;
  ```

- Index 索引 和表平级 提高检索的速度但修改和删除的速度会变慢

  ```sql
  CREATE INDEX idx_name ON table_name(column);
  -- CREATE INDEX idx_name ON db_day04.employee(name);
  ```
  
  ```sql
  DROP INDEX idx_name ON table_name;
  ```
  
  ```sql
  SHOW INDEX FROM table_name;
  ```
  
  - primary key > index 主键自动变成索引
  - unique > index  唯一约束自动变成索引
  - foreign key > index (only for InnoDB 仅仅mysql的这个引擎外键变成索引)
      > [Does MySQL index foreign key columns automatically?](http://stackoverflow.com/questions/304317/does-mysql-index-foreign-key-columns-automatically)

  - 单列索引 `todo`
  - 组合索引 `todo`

### 2. DML 插入 删除 修改对应的语句

> Data Manipulate Language 数据操作语言

- Insert 

  > [没有什么区别 what is difference between insert `VALUE` and insert `VALUES` in mysql statement?](http://stackoverflow.com/a/17445644)
  
  ```sql
  INSERT INTO table_name
  VALUES (value1,value2,value3,...);
  ```

  ```sql
  INSERT INTO table_name (column1,column2,column3,...)
  VALUES (value1,value2,value3,...);
  ```

- Update 更新

  ```sql
  UPDATE table_name
  SET column1=value1,column2=value2,...
  WHERE some_column=some_value;
  ```

- Delete 删除

  ```sql
  DELETE FROM table_name
  WHERE some_column=some_value;
  ```

  > MySQL dump and import

  - import 导入一个数据库
  
    ```sql
    mysql> source file_name.sql
    ```
    
  - load 
  
    ```sql
    LOAD DATA LOCAL INFILE 'path_to_your_csv_file'
    INTO TABLE your_db.your_table
    FIELDS TERMINATED BY ',' (column_name1, column_name2, ...)
    SET id = NULL;
    ```
  - dump 导出数据库
  
    ```sql
    -- your_mysql_directory/bin
    mysqldump -B -u your_mysql_username -p database_name > file_name.sql
    ```

### 3. DQL 比较重要 比较多

> Data Query Language 数据查询语言

- MySQL Show
  - SHOW DATABASES; `显示服务器中所有的库`
  - SHOW TABLES; `显示库中所有的表`
  - SHOW TABLE STATUS FROM database_name; `显示库中所有表的信息`
  - SHOW TABLE STATUS WHERE Name = 'table_name'; `显示表的信息`
  - SHOW [FULL] COLUMNS FROM table_name; `显示表中所有列的信息`
  - SHOW TABLE STATUS WHERE Name = 'table_name'; `显示表的信息`
  - SHOW FULL TABLES FROM database_name; `显示库中的表和视图`
  - SHOW VARIABLES; `显示变量`
  - SHOW CREATE TABLE table_name; `显示建表语句`
  - SHOW CREATE VIEW view_name; `显示建视图语句`
  - SHOW INDEX FROM table_name; `显示表中索引信息`

- SQL select

  ```sql
  SELECT column_name,column_name
  FROM table_name;
  ```

- SQL distinct 唯一的 去除重复的值

  ```sql
  SELECT DISTINCT column_name,column_name
  FROM table_name;
  ```

- SQL where

  > 行检索
  
  ```sql
  SELECT column_name,column_name
  FROM table_name
  WHERE column_name operator value;
  ```

  - <>  表示不等于
  - `BINARY`  区分大小写查询
  
- SQL AND & OR

  ```sql
  SELECT * FROM Customers
  WHERE Country='Germany'
  AND City='Berlin';
  ```
  
  ```sql
  SELECT * FROM Customers
  WHERE City='Berlin'
  OR City='München';
  ```
  
  ```sql
  SELECT * FROM Customers
  WHERE Country='Germany'
  AND (City='Berlin' OR City='München');
  ```
  
- SQL Order By 排序 默认是升序排列

  ```sql
  SELECT column_name1, column_name2
  FROM table_name
  ORDER BY column_name1 ASC|DESC, column_name2 ASC|DESC;
  -- ORDER BY 1, 2  按第几列的升序排列
  ```
  
  > `NUll` min  默认值最小
  
- SQL Top `limit`  分页查询

  ```sql
  SELECT column_name(s)
  FROM table_name
  LIMIT number1 OFFSET number2;
  -- LIMIT number2, number1  其他写的方法
  ```
  
  `LIMIT` 位于 `ORDER BY` 之后
  
- SQL Like  模糊匹配

  ```sql
  SELECT column_name(s)
  FROM table_name
  WHERE column_name [NOT] LIKE pattern;
  ```
  
  > [Copy table without copying data, the keys and indexes are copied over as, well.](http://stackoverflow.com/a/18710438)
  
  ```sql
  CREATE TABLE table_name_new LIKE table_name
  ```
  
- SQL 通配符 
  - `%`  代表字符串
  - `_`  代表一个字符
  - `ESCAPE`   这个没有用
    
    ```sql
    
    SELECT *
    FROM table_name
    WHERE column_name LIKE '%\_%' ESCAPE '\\';-- 正则表达式
    ```
 
- MySQL RLIKE REGEXP 关键字两个意思一样 正则表达式 

- SQL In

  ```sql
  SELECT column_name(s)
  FROM table_name
  WHERE column_name [NOT] IN (value1,value2,...);-- 确定取值的范围
  ```
  
- SQL Between And

  ```sql
  SELECT column_name(s)
  FROM table_name
  WHERE column_name [NOT] BETWEEN value1 AND value2;-- 确定取值的范围
  ```
  
- SQL Aliases 别名

  ```sql
  SELECT column_name [AS] alias_name
  FROM table_name;  -- 列名用别名
  ```
  
  ```sql
  SELECT alias_name.column_name(s)
  FROM table_name [AS] alias_name  -- 表名用别名
  ```
- SQL Nulls 判断

    > `IS [NOT] NULL`   判断是否是空值
    
- SQL ifnull(,)    函数判断运算时是否是空值
- SQL Join 多表查询 联合查询

  > SQL joins are used to combine rows from two or more tables.
 
  > 连接条件 = N - 1

  1. `CROSS JOIN 笛卡儿积 交叉连接` 
  2. `INNER JOIN 内连接`
  3. `OUTER JOIN 外连接`
    - `LEFT OUTER JOIN 左外连接`
    - `RIGHT OUTER JOIN 右外连接`
    - `FULL OUTER JOIN 显示左表T1、右表T2两边中的所有行，即把左联结果表 + 右联结果表组合在一起，然后过滤掉重复的。`

- SQL Cross Join

  > 笛卡儿积

  ```sql
  SELECT column_name(s)
  FROM table1
  [INNER | CROSS] JOIN table2;
  ```

- SQL Inner Join 内连接  返回两个表中具有匹配值的记录 不匹配的就不返回了

  ```sql
  SELECT column_name(s)
  FROM table1
  [INNER] JOIN table2
  ON table1.column_name=table2.column_name;
  ```
  
  - 
  ```sql
  SELECT column_name(s)
  FROM table1
  [INNER] JOIN table2
  USING (column_name); -- For same column_name  主键和外键的名字一样的情况下使用
  ```
  
- SQL Left Join  返回左表中的所有记录，以及右表中匹配的记录 左表中不匹配的用空值替代

  ```sql
  SELECT column_name(s)
  FROM table1
  LEFT [OUTER] JOIN table2
  ON table1.column_name=table2.column_name [AND]
  [WHERE ...];
  ```
  
    - `ON` 条件用来决定如何从 `table_b` 中检索数据行
    - 如果 `table_b` 中没有任何一行数据匹配 `ON` 条件，`将会额外生成一行所有列为 `NULL` 的数据`
    - 在匹配阶段 `WHERE` 子句的条件都不会被使用
    - 在匹配阶段完成以后 `WHERE` 子句条件才会被使用，它将从匹配阶段产生的结果集进行行检索

- SQL Right Join  右联合查询  从右表中返回所有记录，并从左表中返回匹配的记录 右表中不匹配的用空值替代

  ```sql
  SELECT column_name(s)
  FROM table1
  RIGHT [OUTER] JOIN table2
  ON table1.column_name=table2.column_name;
  ```
  
- ~~SQL Full Join~~   `UNION`  两个查询语句查询结果的并集 去掉重复的
- SQL Union

  ```sql
  SELECT column_name(s) FROM table1
  UNION
  SELECT column_name(s) FROM table2;
  -- 会自动去除重复的列  两个查询语句查询结果的并集  不去掉重复的
  ```
  
  ```sql
  SELECT column_name(s) FROM table1
  UNION ALL
  SELECT column_name(s) FROM table2;
  -- 不去除重复的列
  ```
  
- SQL Create Table Select  用选中的列建表

  ```sql
  CREATE TABLE new_table_name
  SELECT * FROM original_table_name;
  ```
- SQL Insert Into Select 插入选中的语句

  ```sql
  INSERT INTO table2
  (column_name(s))
  SELECT column_name(s)
  FROM table1;
  ```
  
- SQL View  就是一个虚表

  > 被存储的查询

  ```sql
  -- 创建视图 或更新视图
  CREATE [OR REPLACE] VIEW view_name AS
  SELECT column_name(s)
  FROM table_name
  WHERE condition;
  ``` 
  
  ```sql
  -- 查询视图 的数量
  SHOW FULL TABLES IN database_name WHERE TABLE_TYPE LIKE 'VIEW';
  ```
  
  ```sql
  -- 删除视图  
  DROP VIEW view_name;
  ```
  1. 简单视图 `updatable view`
      - `简单查询` 生成的，可以修改基表的数据
  2. 复杂视图 `read-only view` 只读视图
      - `复杂查询` 生成的，不可以修改基表的数据    
        - 聚合函数
        - `DISTINCT`
        - `GROUP BY`
        - `HAVING`
        - `UNION` 或 `UNION ALL`
        - `Subquery 子查询`
        - 某些联合查询 (see additional join discussion later in this section)
        - 在 `FROM` 子句中引用不可更新视图
        - Subquery in the WHERE clause that refers to a table in the FROM clause
        - 仅引用了字面值 (在此情况下，没有可以更新的表)
        - 使用 `ALGORITHM = TEMPTABLE` 创建的视图
        - 对基表的任何列有多个引用
        
  3. 视图的作用
      - 数据安全性  只显示安全数据
      - 简化查询 变联合查询为简单查询
      - 逻辑独立性 视图对应业务逻辑

- 子查询 `Sub Queries`

  > 查询的嵌套

  - 相关子查询 `correlated sub query`  子查询不可以独立存在
  - 非相关子查询 `uncorrelated sub query`   子查询可以独立存在

### 4. DTL

  > Data Transaction Language 数据事务语言

  > 在数据库系统中，一个事务是指：由一系列数据库操作组成的一个完整的逻辑过程
  
  - 事务的 `ACID` 特性
    - 原子性 `Atomicity` ` [ˌætəm'ɪsɪti]	`
      - 一个事务 `transaction` 中的所有操作，要么全部完成，要么全部不完成，不会结束在中间某个环节
    - 一致性 `Consistency`
      - 在事务开始之前和事务结束以后，数据库的完整性没有被破坏
    - **隔离性** `Isolation`
      - 数据库允许多个并发事务对其数据进行读写和修改的能力，隔离性可以防止多个事务并发执行时由于交叉执行而导致数据的不一致
    - 持久性 `Durability`
      - 事务处理结束后，对数据的修改就是永久的，即便系统故障也不会丢失
  - 开启一次事务
    - `START TRANSACTION;`
  - 事务处理语句
    - `DML` 语句 `insert` `update` `delete`
    - `DQL` 语句与事务无关 查询语句  不修改数据
  - 显式结束事务
    - `COMMIT;` `提交` 
    - `ROLLBACK;` `回滚`
  - 隐式结束事务
    - `DDL` 语句 以提交方式结束语句
  - 事务保留点
  ```sql
  SAVEPOINT save_point_name; -- 设置保留点
  ROLLBACK TO save_point_name; -- 回滚到保留点，不能结束事务
  ```
  
  ```sql
  SET AUTOCOMMIT = 0;
  SET AUTOCOMMIT = 1;
  ```
<h1 id="20171219_1">数据控制语言</h1>

### 5. DCL  dba 数据库管理员

> Data Control Language 数据控制语言

1. 创建用户

    ```sql
    -- 创建用户
    CREATE USER your_username@'localhost' IDENTIFIED BY 'some_password';
    -- 改用户名
    RENAME USER your_username@'localhost' TO new_your_username@'localhost';
    -- 更改密码
    SET PASSWORD [FOR your_username] = PASSWORD('new_your_password');
    -- 删除用户
    DROP USER your_username;
    ```

2. 权限

    ```sql
    -- 显示权限信息
    SHOW GRANTS FOR your_username@'localhost';
    -- 授予权限
    GRANT some_privileges ON some_databases(some_tables) TO some_users@'localhost';
    -- 撤销权限
    REVOKE some_privileges ON some_databases(some_tables) FROM some_users@'localhost';
    -- 刷新权限
    FLUSH PRIVILEGES;
    -- 权限粒度
    GRANT ALL
    REVOKE ALL 
    ON database_name.*
    ON database_name.table_name
    ```
    
3. MySQL 权限列表

|Privilege|Column|Context|
|---------|------|-------|
|CREATE|Create_priv|databases, tables, or indexes|
|DROP|Drop_priv|databases, tables, or views|
|GRANT OPTION|Grant_priv|databases, tables, or stored routines|
|LOCK TABLES|Lock_tables_priv|databases| 
|REFERENCES|References_priv|databases or tables| 
|EVENT|Event_priv|databases|
|ALTER|Alter_priv|tables| 
|DELETE|Delete_priv|tables|
|INDEX|Index_priv|tables| 
|INSERT|Insert_priv|tables or columns|
|SELECT|Select_priv|tables or columns|
|UPDATE|Update_priv|tables or columns|
|CREATE TEMPORARY TABLES|Create_tmp_table_priv|tables| 
|TRIGGER|Trigger_priv|tables|
|CREATE VIEW|Create_view_priv|views|
|SHOW VIEW|Show_view_priv|views|
|ALTER ROUTINE|Alter_routine_priv|stored routines|
|CREATE ROUTINE|Create_routine_priv|stored routines|
|EXECUTE|Execute_priv|stored routines|
|FILE|File_priv|file access on server host|
|CREATE TABLESPACE|Create_tablespace_priv|server administration|
|CREATE USER|Create_user_priv|server administration|
|PROCESS|Process_priv|server administration|
|PROXY|see proxies_priv table|server administration| 
|RELOAD|Reload_priv|server administration|
|REPLICATION CLIENT|Repl_client_priv|server administration|
|REPLICATION SLAVE|Repl_slave_priv|server administration|
|SHOW DATABASES|Show_db_priv|server administration|
|SHUTDOWN|Shutdown_priv|server administration| 
|SUPER|Super_priv|server administration|
|ALL [PRIVILEGES]||server administration|
|USAGE|-|server administration|

### SQL 函数

  - Aggregate function `聚合函数`
      - AVG(col) `返回指定列的平均值`
      - COUNT(col) `返回指定列中非NULL值的个数`
      - MIN(col) `返回指定列的最小值`
      - MAX(col) `返回指定列的最大值`
      - SUM(col) `返回指定列的所有值之和`
      - GROUP_CONCAT(col) `返回由属于一组的列值连接组合而成的结果`
      - ~~FIRST()~~
      - ~~LAST()~~
      
   - **SQL Group By** `分组查询`

        ```sql
        SELECT aggregate_function(column_name)
        GROUP BY cloumn_name;
        ```
   
      > 把 column_name 列值相同的分为一组
      
      - HAVING `组检索`

      - GROUP_CONCAT([DISTINCT] column_name [Order BY ASC/DESC column_name] [Separator '分隔符'])
      
        ```sql
        SET group_concat_max_len = 2048 -- default 1024
        ```

  - Scalar function 标量函数 

    - 数学函数
        - ABS(x) `返回 x 的绝对值`
        - BIN(x) `返回 x 的二进制（OCT 返回八进制，HEX 返回十六进制）`
        - CEILING(x) `返回大于 x 的最小整数值`
        - EXP(x) `返回值 e（自然对数的底）的 x 次方`
        - FLOOR(x) `返回小于 x 的最大整数值`
        - GREATEST(x1,x2,...,xn) `返回集合中最大的值`
        - LEAST(x1,x2,...,xn) `返回集合中最小的值`
        - LN(x) `返回 x 的自然对数`
        - LOG(x,y) `返回 x 的以 y 为底的对数`
        - MOD(x,y) `返回 x / y 的模（余数）`
        - PI() `返回 PI 的值（圆周率）`
        - RAND() `返回 ０ 到 １ 内的随机值,可以通过提供一个种子参数使随机数生成器生成一个指定的值`
        - ROUND(x,y) `返回参数 x 的四舍五入的有 y 位小数的值`
        - SIGN(x) `返回代表数字 x 的符号的值`
        - SQRT(x) `返回一个数的平方根`
        - TRUNCATE(x,y) `返回数字 x 截短为 y 位小数的结果`
    
    - 字符串函数
        - ASCII(char) `返回字符的 ASCII 码值`
        - BIT_LENGTH(str) `返回字符串的比特长度`
        - CONCAT(s1,s2...,sn) `将 s1,s2...,sn 连接成字符串`
        - CONCAT_WS(sep,s1,s2...,sn) `将 s1,s2...,sn 连接成字符串，并用 sep 字符间隔`
        - INSERT(str,x,y,instr) `将字符串 str 从第 x 位置开始，y 个字符长的子串替换为字符串 instr`
        - FIND_IN_SET(str,list) `分析逗号分隔的 list 列表，如果发现 str，返回 str 在 list 中的位置`
        - LCASE(str)或LOWER(str) `返回将字符串 str 中所有字符改变为小写后的结果`
        - LEFT(str,x) `返回字符串 str 中最左边的 x 个字符`
        - LENGTH(s) `返回字符串 str 中的字符数`
        - LTRIM(str) `从字符串 str 中切掉开头的空格`
        - POSITION(substr,str) `返回子串 substr 在字符串 str 中第一次出现的位置`
        - QUOTE(str) `用反斜杠转义 str 中的单引号`
        - REPEAT(str,srchstr,rplcstr) `返回字符串 str 重复 x 次的结果`
        - REVERSE(str) `返回颠倒字符串 str 的结果`
        - RIGHT(str,x) `返回字符串 str 中最右边的 x 个字符`
        - RTRIM(str) `返回字符串 str 尾部的空格`
        - STRCMP(s1,s2) `比较字符串 s1 和 s2`
        - TRIM(str) `去除字符串首部和尾部的所有空格`
        - UCASE(str)或UPPER(str) `返回将字符串 str 中所有字符转变为大写后的结果`
            
    - 日期和时间函数
        - CURDATE()或CURRENT_DATE() `返回当前的日期`
        - CURTIME()或CURRENT_TIME() `返回当前的时间`
        - DATE_ADD(date,INTERVAL int keyword) `返回日期 date 加上间隔时间 int 的结果`
        - DATE_FORMAT(date,fmt) `依照指定的 fmt 格式格式化日期 date 值`
        - DATE_SUB(date,INTERVAL int keyword) `返回日期 date 加上间隔时间 int 的结果`
        - DAYOFWEEK(date) `返回 date 所代表的一星期中的第几天(1~7)`
        - DAYOFMONTH(date) `返回 date 是一个月的第几天(1~31)`
        - DAYOFYEAR(date) `返回 date 是一年的第几天(1~366)`
        - DAYNAME(date) `返回 date 的星期名，如：SELECT DAYNAME(CURRENT_DATE);`
        - FROM_UNIXTIME(ts,fmt) `根据指定的 fmt 格式，格式化 UNIX 时间戳 ts`
        - HOUR(time) `返回 time 的小时值(0~23)`
        - MINUTE(time) `返回 time 的分钟值(0~59)`
        - MONTH(date) `返回 date 的月份值(1~12)`
        - MONTHNAME(date) `返回 date 的月份名`
        - NOW() `返回当前的日期和时间`
        - QUARTER(date) `返回 date 在一年中的季度(1~4)`
        - WEEK(date) `返回日期 date 为一年中第几周(0~53)`
        - YEAR(date) `返回日期 date 的年份(1000~9999)`