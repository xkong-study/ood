为什么 MySQL 不建议使用 NULL 作为列默认值？       
数据完整性：     
不确定性：NULL 表示未知的值，导致数据中存在歧义或不确定性，尤其是在比较和聚合操作时。     
逻辑问题：这种不确定性在执行查询中的条件逻辑或比较时会引起问题，因为 NULL 与空字符串或其他值的行为不同。     

性能开销：      
索引问题：NULL 值可能无法被高效地索引，在查询或筛选时可能影响性能。    
存储影响：虽然 NULL 在列的值存储上会节省空间，但它需要额外的元数据空间来记录这个字段为 NULL。      

聚合影响：     
结果错误：聚合函数如 SUM、AVG、MIN 和 MAX 会忽略 NULL 值，这种行为可能导致计算结果不准确，影响数据分析。     
COUNT 行为：COUNT 函数的行为取决于参数。COUNT(*) 会统计包括 NULL 在内的所有记录数，而 COUNT(列名) 仅统计非 NULL 值。这种差异可能会导致计数逻辑的不一致。      

替代方案：      
默认值：比起 NULL，可以考虑使用合适的默认值，比如 0、空字符串或根据业务逻辑定义的特殊标记值。     
明确约束：强制使用 NOT NULL 约束，并设置合适的默认值，可以使数据更清晰，简化查询并改善应用逻辑。       

Boolean 类型如何表示？     
MySQL 中没有专门的布尔类型，而是用 TINYINT(1) 类型来表示布尔值。TINYINT(1) 类型可以存储 0 或 1，分别对应 false 或 true。    

不同存储引擎的主要区别不仅在于存储方式不同，还包括其他几个关键的方面，比如索引机制、事务处理、锁定策略以及数据恢复能力。这些因素共同影响着不同存储引擎在实际应用中的表现。以下是对这些差异的详细解释：

数据存储方式：     
InnoDB：使用聚集索引，将数据和主键索引存储在同一结构中。表和索引文件可以分开管理。        
MyISAM：数据和索引存储在独立的文件中，索引指向数据文件中的物理位置。     
Memory：数据全部存储在内存中，不持久化到磁盘。     
Archive：以压缩的形式存储数据，适用于归档操作。       

索引机制：   
InnoDB：支持主键索引和辅助索引，主键索引是聚集索引。     
MyISAM：支持全文索引和B-Tree索引，不支持外键。     
Memory：通常使用哈希索引，也可使用B-Tree索引。      
Archive：通常不支持索引，适用于大量数据归档。    

事务处理：  
InnoDB：支持事务，遵循 ACID 原则，并具有崩溃恢复能力。     
MyISAM：不支持事务。  
Memory：不支持事务。     
Archive：不支持事务。     

锁定策略： 
InnoDB：使用行级锁，适合高并发环境。      
MyISAM：使用表级锁，读密集型操作更高效。      
Memory：使用表级锁。          
Archive：行级锁，读取归档数据。               

恢复能力：   
InnoDB：具有强大的崩溃恢复功能，数据一致性高。     
MyISAM：恢复能力有限，不具备自动恢复特性。     
Memory：由于数据存储在内存中，断电会导致数据丢失。            
Archive：压缩数据较难恢复。         

MyISAM 和 InnoDB 有什么区别？     

1、是否支持行级锁？      
MyISAM 只有表级锁(table-level locking)，而 InnoDB 支持行级锁(row-level locking)和表级锁,默认为行级锁。也就说，MyISAM 一锁就是锁住了整张表，这在并发写的情况下是多么滴憨憨啊！这也是为什么 InnoDB 在并发写的时候，性能更牛皮了！      

2、是否支持事务？     
MyISAM 不提供事务支持。InnoDB 提供事务支持，实现了 SQL 标准定义了四个隔离级别，具有提交(commit)和回滚(rollback)事务的能力。并且，InnoDB 默认使用的 REPEATABLE-READ（可重读）隔离级别是可以解决幻读问题发生的（基于 MVCC 和 Next-Key Lock）。关于 MySQL 事务的详细介绍，可以看看我写的这篇文章：MySQL 事务隔离级别详解。    

可重读性（Repeatable Read）     
定义：在一个事务的整个过程中，多次读取相同的记录会得到相同的结果，即使其他事务同时对这些记录进行了更新。     
目的：确保一个事务读取的数据在该事务期间保持一致，不受其他事务的更新操作影响。     

问题：可重读性无法解决插入的新记录，即“幻读”问题。      

幻读（Phantom Read）       
定义：当一个事务在处理数据期间，两次执行相同的查询语句会得到不同的结果。因为其他事务在期间插入或删除了满足条件的新记录，这些新出现的或消失的记录称为“幻影”。      
例子：    
场景：在事务 A 中，查询所有的客户记录。     
现象：在事务 A 尚未结束时，事务 B 新增了符合事务 A 查询条件的记录。当事务 A 再次查询时，新记录会“幻影般”出现。    

那怎么实现这两个功能呢？      

1. 启用多版本并发控制（MVCC）

设置隔离级别：为了使用 MVCC，事务的隔离级别应设置为可重复读 (REPEATABLE READ) 或更高。InnoDB 默认的隔离级别已经是可重复读。

```code
SET SESSION TRANSACTION ISOLATION LEVEL REPEATABLE READ;
```
事务操作：开始一个事务，随后执行查询和其他操作。在事务开始后，所有的读取操作都将看到事务开始时的数据状态，不会受到其他事务的影响。

```code
START TRANSACTION;

SELECT * FROM my_table WHERE condition;

-- 事务内的其他操作

COMMIT;
```

自动化：InnoDB 自动维护数据的多个版本和时间戳，开发者无需额外操作。     

2. 启用 Next-Key Lock（下一键锁）

自动启用：Next-Key Lock 是 InnoDB 默认的锁定机制，在 REPEATABLE READ 隔离级别下自动启用。    
注意事项：以下操作可以确保锁定机制有效：     
范围查询：Next-Key Lock 在范围查询（如 BETWEEN、>, <）中生效，以锁定行和相邻的间隙。     
唯一索引：如果查询条件基于唯一索引，InnoDB 仅会对该索引匹配的行使用行锁，而不涉及间隙锁。    
更新和删除：更新或删除操作会锁定目标行及其相邻的间隙，以防止其他事务并发修改。       

例子：     

```code
START TRANSACTION;

-- 范围查询加锁，防止其他事务插入新的符合条件的记录
SELECT * FROM my_table WHERE id BETWEEN 10 AND 20 FOR UPDATE;

-- 执行其他需要在锁定范围内的操作

COMMIT;
```

在这些操作中，InnoDB 引擎将自动应用 MVCC 和 Next-Key Lock，以确保事务的可重复读和防止幻读问题。       

不得使用外键与级联，一切外键概念必须在应用层解决。    

使用外键约束的方式（数据库层）：    

```code
-- 创建 customers 表
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100)
);

-- 创建 orders 表，带有外键约束
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    product VARCHAR(100),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id) ON DELETE CASCADE
);

-- 删除某个客户
DELETE FROM customers WHERE customer_id = 1;

```

在应用层解决（无外键约束）    
如果不使用外键约束和级联删除，而在应用层解决这个问题：   

```code
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class DeleteCustomerAndOrders {

    // 数据库连接信息
    private static final String DB_URL = "jdbc:mysql://localhost:3306/your_database";
    private static final String USER = "your_username";
    private static final String PASS = "your_password";

    public static void main(String[] args) {
        int customerIdToDelete = 1;  // 需要删除的客户 ID
        deleteCustomerAndOrders(customerIdToDelete);
    }

    // 删除指定客户及其相关订单
    public static void deleteCustomerAndOrders(int customerId) {
        Connection conn = null;
        PreparedStatement deleteOrdersStmt = null;
        PreparedStatement deleteCustomerStmt = null;

        try {
            // 获取数据库连接
            conn = DriverManager.getConnection(DB_URL, USER, PASS);
            // 关闭自动提交，开启事务
            conn.setAutoCommit(false);

            // 删除与客户相关的订单
            String deleteOrdersSQL = "DELETE FROM orders WHERE customer_id = ?";
            deleteOrdersStmt = conn.prepareStatement(deleteOrdersSQL);
            deleteOrdersStmt.setInt(1, customerId);
            deleteOrdersStmt.executeUpdate();

            // 删除客户记录
            String deleteCustomerSQL = "DELETE FROM customers WHERE customer_id = ?";
            deleteCustomerStmt = conn.prepareStatement(deleteCustomerSQL);
            deleteCustomerStmt.setInt(1, customerId);
            deleteCustomerStmt.executeUpdate();

            // 提交事务
            conn.commit();
            System.out.println("Successfully deleted customer and associated orders.");

        } catch (SQLException e) {
            // 出现异常，进行回滚
            if (conn != null) {
                try {
                    conn.rollback();
                } catch (SQLException ex) {
                    ex.printStackTrace();
                }
            }
            e.printStackTrace();
        } finally {
            // 关闭资源
            if (deleteOrdersStmt != null) {
                try {
                    deleteOrdersStmt.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (deleteCustomerStmt != null) {
                try {
                    deleteCustomerStmt.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (conn != null) {
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}

```


MySQL 查询缓存：     

执行查询语句的时候，会先查询缓存。不过，MySQL 8.0 版本后移除，因为这个功能不太实用       

my.cnf 加入以下配置，重启 MySQL 开启查询缓存：     

```code
query_cache_type=1
query_cache_size=600000
```

