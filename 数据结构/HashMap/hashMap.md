hashCode 和 equals 是 Java 中用于处理对象相等性的两个方法，它们有不同的作用：   
 
hashCode 方法：    
 
hashCode 方法返回一个对象的哈希码（32 位整数），用于确定对象在哈希表中的存储位置。    
由于哈希表的存储位置是通过哈希码计算得出的，相等的对象应该具有相等的哈希码，但相等哈希码的对象并不一定相等。    
equals 方法：    

equals 方法用于判断两个对象是否相等，即它们在逻辑上是否表示相同的实体。      
如果 equals 方法被重写，它应该满足以下条件：         
自反性：对于任何非空引用 x，x.equals(x) 应该返回 true。       
对称性：对于任何非空引用 x 和 y，如果 x.equals(y) 返回 true，那么 y.equals(x) 也应该返回 true。        
传递性：对于任何非空引用 x、y 和 z，如果 x.equals(y) 返回 true，且 y.equals(z) 也返回 true，那么 x.equals(z) 也应该返回 true。       
一致性：对于任何非空引用 x 和 y，多次调用 x.equals(y) 应该始终返回相同的结果，只要对象上的信息没有被修改。        
在使用哈希表等数据结构时，hashCode 方法主要用于确定存储位置，而 equals 方法用于比较对象的逻辑相等性。在一般情况下，如果两个对象的 equals 方法返回 true，那么它们的 hashCode 方法应该返回相同的值，但反之不一定成立。        

哈希表（Hash Table）是一种常用的数据结构，用于实现关联数组或映射。它通过哈希函数将键映射到表中的位置，以加快对键值对的访问速度。哈希表是一种效率高、平均查找时间复杂度为 O(1) 的数据结构。         

基本思想是将键通过哈希函数转换成一个索引，然后将值存储在该索引对应的位置。当需要查找、插入或删除时，再次使用哈希函数找到对应的索引，从而快速访问数据。       

哈希表的基本操作包括：      

插入（Insert）： 将键值对插入到哈希表中，根据哈希函数找到对应的位置。  

查找（Search）： 根据键查找对应的值，通过哈希函数找到对应的位置，然后检查该位置的值。

删除（Delete）： 根据键删除哈希表中的值，通过哈希函数找到对应的位置，然后将该位置的值置为空或使用特殊标记表示删除。

哈希表的性能取决于哈希函数的设计和解决冲突的方法。解决冲突的常见方法包括链地址法（Chaining）和开放寻址法（Open Addressing）。在实际应用中，哈希表被广泛用于实现字典、集合等数据结构，以及数据库索引等场景。

```code
        Map<String, Integer> hashMap = new HashMap<>();

        // 插入键值对
        hashMap.put("Alice", 25);
        hashMap.put("Bob", 30);
        hashMap.put("Charlie", 22);

        // 查找键对应的值
        int ageOfAlice = hashMap.get("Alice");
        System.out.println("Age of Alice: " + ageOfAlice);

        // 删除键值对
        hashMap.remove("Bob");

        // 再次查找 Bob
        Integer ageOfBob = hashMap.get("Bob");
```
Java Map 操作表，put remove 不可少。

JavaScript Map 在场，set delete ，SetAdd记得牢。

Set add 增加光，remove 删除行。
