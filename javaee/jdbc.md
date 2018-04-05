# Chapter 8 JDBC

> Java Database Connectivity java连接数据库

## java.sql.*

1. `Driver` Interface  这个是接口，使用它的实现类
2. `DriverManager` Class
3. `Connection` Interface
4. `Statement` Initerface
5. `PreparedStatement` Interface  使用这个子接口
6. `CallableStatement` Interface
6. `ResultSet` Interface  查询结果集
7. `DatabaseMetaData` Interface 和数据库有关的接口

## JDBC Transaction  事务

```java
public class TransactionTest {
    public static void main(String[] args) {
        Connection connection = Db.getConnection();
        PreparedStatement preparedStatement = null;
        try {
            
            if (connection == null) {
                return;
            }

            connection.setAutoCommit(false); // 关闭自动提交：开启一次 JDBC 事务

            /*
                DML 操作：INSERT UPDATE DELETE
             */

            connection.commit(); // 正常：提交
        } catch (Exception e) {
            e.printStackTrace();
            try {
                connection.rollback(); // 异常：回滚
                connection.setAutoCommit(true); // 重置为自动提交
            } catch (SQLException sql) {
                sql.printStackTrace();
            }
        } finally {
            Db.close(null, preparedStatement, connection);
        }
    }
}

```

## SQL Injection 

> SQL 注入   
Statement 注入风险 因为字符串采用拼装的方式写sql语句