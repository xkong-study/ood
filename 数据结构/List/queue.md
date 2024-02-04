Queue 接口是一个继承自 Collection 接口的子接口，它表示一种队列数据结构，采用先进先出（FIFO）的原则。以下是 Queue 接口中一些常用的方法：   
 
添加元素：   
   
boolean add(E e): 将指定的元素插入此队列（如果立即可行且不会违反容量限制），成功时返回 true，如果当前没有可用的空间，则抛出异常。   
boolean offer(E e): 将指定的元素插入此队列（如果立即可行且不会违反容量限制），成功时返回 true，如果当前没有可用的空间，则返回 false。   
移除元素：

E remove(): 获取并移除队列头部的元素，如果队列为空，则抛出异常。   
E poll(): 获取并移除队列头部的元素，如果队列为空，则返回 null。   
E element(): 获取但不移除队列头部的元素，如果队列为空，则抛出异常。  
E peek(): 获取但不移除队列头部的元素，如果队列为空，则返回 null。   
检查队列状态：   

int size(): 返回队列中的元素数量。   
boolean isEmpty(): 如果队列为空，返回 true；否则，返回 false。    
其他方法：   
   
boolean contains(Object o): 如果队列包含指定的元素，则返回 true。   
Iterator<E> iterator(): 返回队列元素的迭代器。   
Object[] toArray(): 将队列中的元素转换为数组。  
