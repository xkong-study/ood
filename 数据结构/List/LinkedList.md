LinkedList 是 Java 中的一个双向链表实现的类。它实现了 List 接口，允许元素插入和删除时维护元素的顺序。    

以下是 LinkedList 的一些特点和常用方法：     

双向链表： LinkedList 使用双向链表来存储元素，每个节点都包含指向前一个节点和后一个节点的引用，这使得在链表中进行插入和删除操作更加高效。    

非同步： LinkedList 不是线程安全的，它不支持多线程并发访问。如果需要在多线程环境下使用，可以考虑使用 Collections.synchronizedList 方法包装成线程安全的列表。   

允许 null 元素： LinkedList 允许存储 null 元素。    

随机访问较慢： 由于 LinkedList 是基于链表实现的，因此随机访问元素的效率相对较低。如果需要频繁随机访问元素，建议使用 ArrayList。    

常用方法：    

addFirst(E e): 在链表头部插入元素。    
addLast(E e): 在链表尾部插入元素。    
removeFirst(): 移除链表头部的元素。   
removeLast(): 移除链表尾部的元素。   
getFirst(): 获取链表头部的元素。    
getLast(): 获取链表尾部的元素。    
add(int index, E element): 在指定位置插入元素。    
remove(int index): 移除指定位置的元素。    

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
