LinkedHashMap 是在 HashMap 的基础上使用链表维护插入顺序或访问顺序的。它通过一个双向链表连接了所有的条目，这样可以按照插入顺序或者最近访问顺序（access-order）进行迭代。       
注意该循环双向链表的头部存放的是最久访问的节点或最先插入的节点，尾部为最近访问的或最近插入的节点，迭代器遍历方向是从链表的头部开始到链表尾部结束，在链表尾部有一个空的header节点，该节点不存放key-value内容，为LinkedHashMap类的成员属性，循环双向链表的入口。      
![截屏2024-02-05 12.10.09.png](https://img.xwyue.com/i/2024/02/05/65c0d02a0dc6e.png)     


按照插入顺序或访问顺序遍历：     

accessOrder 参数控制是否按照访问顺序排序。当 accessOrder 为 true 时，迭代顺序是访问顺序；为 false 时，迭代顺序是插入顺序。     
LinkedHashMap(boolean accessOrder): 指定排序模式的构造方法。    
其他方法：    

clear(): 清空 LinkedHashMap。    
containsKey(Object key): 判断是否包含指定键。    
containsValue(Object value): 判断是否包含指定值。    
get(Object key): 获取指定键对应的值。    
put(K key, V value): 向 LinkedHashMap 中添加键值对。    
remove(Object key): 移除指定键的映射。   
size(): 获取 LinkedHashMap 中键值对的数量。   

```code
import java.util.LinkedHashMap;
import java.util.Map;

public class LinkedHashMapExample {

    public static void main(String[] args) {
        // 创建一个LinkedHashMap，并设置accessOrder为true
        Map<String, Integer> linkedHashMap = new LinkedHashMap<>(16, 0.75f, true);

        // 添加元素
        linkedHashMap.put("one", 1);
        linkedHashMap.put("two", 2);
        linkedHashMap.put("three", 3);

        // 输出初始顺序
        System.out.println("初始顺序：" + linkedHashMap);

        // 访问一个元素
        linkedHashMap.get("two");

        // 输出访问后的顺序
        System.out.println("访问后的顺序：" + linkedHashMap);

        // 再次访问一个元素
        linkedHashMap.get("three");

        // 输出再次访问后的顺序
        System.out.println("再次访问后的顺序：" + linkedHashMap);
    }
}
```

在 LinkedHashMap 的构造函数中，16 是初始容量（initial capacity），0.75f 是负载因子（load factor）。这两个参数影响着 LinkedHashMap 在内部如何处理元素的存储。     

初始容量（initial capacity）： 它是指 LinkedHashMap 内部数组的初始大小。当 LinkedHashMap 中的元素数量达到负载因子与初始容量的乘积时，内部数组会被重新调整大小。初始容量的选择通常考虑到预期的元素数量，以避免频繁的调整数组大小。    

负载因子（load factor）： 它是指 LinkedHashMap 在重新调整大小之前，内部数组的填充程度。负载因子是一个浮点数，通常取值在 0.0 到 1.0 之间。当 LinkedHashMap 中的元素数量达到负载因子与初始容量的乘积时，内部数组会被重新调整大小。负载因子的选择影响着空间利用率和性能之间的权衡。     

