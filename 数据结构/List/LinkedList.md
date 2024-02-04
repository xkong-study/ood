LinkedList 是 Java 中的一个双向链表实现的类。它实现了 List 接口，允许元素插入和删除时维护元素的顺序。    

以下是 LinkedList 的一些特点和常用方法：     

双向链表： LinkedList 使用双向链表来存储元素，每个节点都包含指向前一个节点和后一个节点的引用，这使得在链表中进行插入和删除操作更加高效。    

非同步： LinkedList 不是线程安全的，它不支持多线程并发访问。如果需要在多线程环境下使用，可以考虑使用 Collections.synchronizedList 方法包装成线程安全的列表。   

允许 null 元素： LinkedList 允许存储 null 元素。    

随机访问较慢： 由于 LinkedList 是基于链表实现的，因此随机访问元素的效率相对较低。如果需要频繁随机访问元素，建议使用 ArrayList。    
 
Queue 接口相关方法：       
添加元素到队列尾部：      

boolean offer(E e): 在队列尾部添加元素，成功返回 true，失败返回 false。       
boolean offerFirst(E e): 在队列头部添加元素，成功返回 true，失败返回 false。      
boolean offerLast(E e): 在队列尾部添加元素，成功返回 true，失败返回 false。         
获取并移除队列头部的元素：       
     
E poll(): 获取并移除队列头部的元素，如果队列为空，返回 null。       
E pollFirst(): 获取并移除队列头部的元素，如果队列为空，返回 null。       
E pollLast(): 获取并移除队列尾部的元素，如果队列为空，返回 null。       
获取但不移除队列头部的元素：       

E peek(): 获取但不移除队列头部的元素，如果队列为空，返回 null。       
E peekFirst(): 获取但不移除队列头部的元素，如果队列为空，返回 null。   
E peekLast(): 获取但不移除队列尾部的元素，如果队列为空，返回 null。   
List 接口相关方法：    
添加元素：     

boolean add(E e): 将元素添加到列表的末尾，成功返回 true。   
void add(int index, E element): 在指定位置插入元素。   
获取元素：   

E get(int index): 获取列表中指定位置的元素。   
移除元素：   

boolean remove(Object o): 移除列表中指定元素的第一个匹配项。  
E remove(int index): 移除列表中指定位置的元素。  
其他：  

E set(int index, E element): 用指定的元素替代列表中指定位置的元素。  
List<E> subList(int fromIndex, int toIndex): 返回列表中指定的子列表。  
  

```code
import java.util.LinkedList;

public class Example {
    public static void main(String[] args) {
        LinkedList<String> linkedList = new LinkedList<>();

        // 在链表尾部添加元素
        linkedList.add("Apple");
        linkedList.add("Banana");
        linkedList.add("Orange");

        // 在链表头部添加元素
        linkedList.addFirst("Grapes");

        // 移除链表尾部的元素
        linkedList.removeLast();

        // 获取链表头部的元素
        String firstElement = linkedList.getFirst();

        // 输出链表元素
        System.out.println(linkedList); // 输出：[Grapes, Apple, Banana]
    }
}
```
