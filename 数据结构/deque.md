Deque（Double Ended Queue，双端队列）是一个支持在两端插入和删除元素的队列。在 Java 中，Deque 接口继承了 Queue 接口，提供了丰富的方法。     

以下是 Deque 接口的一些常用方法：   

添加元素：   

addFirst(E e): 在双端队列的开头添加元素。   
addLast(E e): 在双端队列的末尾添加元素。     
offerFirst(E e): 在双端队列的开头添加元素，如果队列已满则返回 false。      
offerLast(E e): 在双端队列的末尾添加元素，如果队列已满则返回 false。      
获取元素：      

getFirst(): 获取双端队列的开头元素，如果队列为空则抛出异常。      
getLast(): 获取双端队列的末尾元素，如果队列为空则抛出异常。      
peekFirst(): 获取双端队列的开头元素，如果队列为空则返回 null。     
peekLast(): 获取双端队列的末尾元素，如果队列为空则返回 null。        
移除元素：       

removeFirst(): 移除双端队列的开头元素，如果队列为空则抛出异常。     
removeLast(): 移除双端队列的末尾元素，如果队列为空则抛出异常。      
pollFirst(): 移除双端队列的开头元素，如果队列为空则返回 null。       
pollLast(): 移除双端队列的末尾元素，如果队列为空则返回 null。         
其他方法：         
   
size(): 返回双端队列中的元素个数。        
isEmpty(): 判断双端队列是否为空。             
iterator(): 返回在此双端队列的元素上以适当顺序进行迭代的迭代器。            

