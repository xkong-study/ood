数组（Array）和列表（List）是两种不同的数据结构，它们在很多方面有着显著的区别。

固定大小 vs. 动态大小:

数组: 在创建时需要指定大小，且一旦创建，大小就不能改变。
列表: 动态调整大小，可以根据需要动态添加或删除元素。
数据类型:

数组: 可以包含基本数据类型（如 int, char）或对象类型，但所有元素的数据类型必须相同。
列表: 通常用于存储对象，可以存储不同数据类型的对象。
内存分配:

数组: 在内存中是连续存储的，访问速度较快，但插入和删除元素可能涉及大量数据移动。
列表: 通常使用链表或动态数组实现，插入和删除元素的开销较小，但访问元素的速度可能较慢。
API 和方法:

数组: 具有固定的API，提供了一些用于访问和修改元素的方法，如 length 属性、clone 方法等。
列表: 由Java集合框架定义，提供了更多的操作方法，如 add、remove、get 等。
编程灵活性:

数组: 需要预先知道数组的大小，不够灵活。
列表: 具有动态大小，更加灵活，适用于不确定大小的情况。

List 接口： 表示一个有序的集合，可以包含重复的元素。List 接口的常见实现类有 ArrayList、LinkedList、Vector 等。List 接口提供了一系列方法，用于操作集合中的元素，例如添加、删除、获取元素等。

Arrays 类： 是 java.util 包中的一个工具类，提供了许多有关数组的静态方法。这些方法包括用于数组排序、查找、复制等操作。Arrays 类还包含了一个 asList 方法，用于将数组转换为固定大小的列表，如前面提到的。


以下是一些常见的 List 接口的方法：     
 
添加元素：     

boolean add(E element): 将指定的元素追加到列表的末尾。     
void add(int index, E element): 将指定的元素插入到列表的指定位置。     

获取元素：     

E get(int index): 返回列表中指定位置的元素。    
int indexOf(Object o): 返回列表中第一次出现指定元素的索引。     
int lastIndexOf(Object o): 返回列表中最后一次出现指定元素的索引。    

删除元素：     

boolean remove(Object o): 从列表中移除指定元素的第一个匹配项。    
E remove(int index): 移除列表中指定位置的元素。    
void clear(): 移除列表中的所有元素。    

替换元素：     

E set(int index, E element): 用指定的元素替换列表中指定位置的元素。      

列表信息：     

int size(): 返回列表中的元素数量。        
boolean isEmpty(): 如果列表不包含元素，则返回 true。    
boolean contains(Object o): 如果列表包含指定的元素，则返回 true。     

子列表：     

List<E> subList(int fromIndex, int toIndex): 返回列表中指定的 fromIndex（包括）和 toIndex（不包括）之间的部分视图。    

迭代和遍历：    
 
Iterator<E> iterator(): 返回在列表的元素上进行迭代的迭代器。    
void forEach(Consumer<? super E> action): 对列表的每个元素执行指定的操作。     
void forEachOrdered(Consumer<? super E> action): 对列表的每个元素按顺序执行指定的操作。     

数组操作：    

Object[] toArray(): 将列表转换为数组。   

