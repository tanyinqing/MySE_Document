- 向表中添加一列

```
ALTER TABLE Persons

ADD COLUMN column_name datatype [AFTER column_name | FIRST];
```
- 主键约束的建表语句‘

```
CREATE TABLE table_name (

  id INT AUTO_INCREMENT PRIMARY KEY,  
     City varchar(255),

);
```
- 建表语句
```
CREATE TABLE Persons (

  P_Id int NOT NULL,

  LastName varchar(255) NOT NULL,

  FirstName varchar(255),

  Address varchar(255),

  City varchar(255),

  PRIMARY KEY (P_Id)

);

```