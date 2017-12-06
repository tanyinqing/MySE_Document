
# 查询数据库的详情
- SHOW DATABASES ;
- SHOW TABLE STATUS FROM scott;   显示表的信息
- SHOW FULL COLUMNS FROM scott.emp;    显示字段的详细信息

# 数据库备份和还原
拷贝数据库 到目录 D:\mysql\bin  导出的操作
- D:
- cd mysql/bin
- mysqldump -B -u root -p db_day03 > file_name.sql

- mysql -u root -p  开启数据库
- source d:\mysql\bin\tan.sql  反向操作把数据库导入服务器
# 主表和从表的关系
- 1_foreign-key 这个练习题
- 主表是主键所在的表  例如 部门表
- 从表是外键所在的表  例如 员工表
- 从表必须包括主表的主键

# ddl 数据库定义语言
- 建立联合查询

```
-- 查询语句 联合查询
SELECT e.NAME,d.title,d.location FROM db_day03.employee e
INNER JOIN db_day03.department d ON e.departmentId=d.id;
```
- 建立外键约束

```
-- 先建立表 在建立外键约束
-- 外键引用了主表中的主键
-- 插入数据是外键可以为空

-- 建立外键约束 必须对应主键才可以 推荐使用
ALTER TABLE db_day03.employee
  ADD CONSTRAINT
  employee_fk_departmentId  -- 外键约束的别名
FOREIGN KEY (departmentId) REFERENCES db_day03.department(id) -- 对应主表的外键
-- ON DELETE CASCADE ;-- 这条选项表明 主表删除 从表引用记录连带删除
-- ON DELETE SET NULL ;-- 这条选项表明 主表删除 从表引用记录连带变成空
-- ON UPDATE SET NULL ;-- 这条选项表明 主表主键修改 从表引用记录连带变成空
ON UPDATE CASCADE ;-- 这条选项表明 主表主键修改 从表引用记录连带改变
-- 如果没有前4相 不允许删除

-- 主键从指定的值开始
ALTER TABLE db_day03.department AUTO_INCREMENT=100;
ALTER TABLE db_day03.employee AUTO_INCREMENT=1000;

SET FOREIGN_KEY_CHECKS =0;-- 使外键失效
SET FOREIGN_KEY_CHECKS =1;-- 使外键生效

-- 删除外键约束
INSERT INTO db_day03.employee VALUE (NULL, 'satt','1990-1-1','999');
ALTER TABLE db_day03.employee DROP FOREIGN KEY employee_fk_departmentId;
```


- 字符串用双引号  年月日用单引号
- 创建数据库的标准语言

```
CREATE DATABASE db_day01;

CREATE TABLE db_day01.student (
  id     INT COMMENT '这个是id',
  name   VARCHAR(255) COMMENT '姓名',
  gender CHAR(1) COMMENT '性别',
  age    INT COMMENT '年龄',
  height DOUBLE(3, 2) COMMENT '身高', -- 小数部分2位 一共有3位
  fee    DECIMAL(6, 2) COMMENT '学费', -- 学费一共6位 小数有2位 涉及到钱 专用
  dob    DATE COMMENT '出生年月日' -- 生日 年月日

)
  COMMENT '学生表';

INSERT INTO db_day01.student VALUE (1, "Tom", "M", 18, 1.75, 1234.56, '1999-1-2'); -- 插入一组数据

SELECT *
FROM db_day01.student; -- 查询学生表

-- 显示某个数据表完整的字段信息
SHOW FULL COLUMNS FROM db_day01.student;

-- 显示某个数据库表的注释
SHOW TABLE STATUS FROM db_day01;
DROP TABLE db_day01.student; -- 删除数据表
DROP DATABASE db_day01; -- 删除数据库
```
