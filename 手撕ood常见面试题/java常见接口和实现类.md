### Collection 接口:

Collection 接口是集合框架的根接口，定义了操作集合的基本方法。
子接口包括 List、Set 和 Queue。

### List 接口:

List 接口表示一个有序的元素集合，允许重复元素。
常见实现类有 ArrayList、LinkedList、Vector。

### Set 接口:

Set 接口表示一个不包含重复元素的集合。
常见实现类有 父类HashSet。
子类 LinkedHashSet（内部使用链表维护元素的插入顺序）、TreeSet。

### Queue 接口:

Queue 接口表示一个队列，支持在队尾添加元素，队头移除元素。
子接口包括 Deque。
常见实现类有 LinkedList、PriorityQueue。

### Deque 接口:

Deque 接口是一个双端队列，支持在两端进行元素的插入和删除操作。
常见实现类有 LinkedList、ArrayDeque。

### Map 接口:

Map 接口表示键值对的映射。
常见实现类有 HashMap、LinkedHashMap、TreeMap。

### SortedMap 接口:

SortedMap 接口继承自 Map 接口，表示一个按键进行排序的映射。
常见实现类有 TreeMap。

### NavigableMap 接口:

NavigableMap 接口继承自 SortedMap，提供了一些额外的导航方法。
常见实现类有 TreeMap。

### Iterator 接口:

Iterator 接口用于遍历集合中的元素。
常见实现类有 ArrayList、LinkedList。

#### 主要方法包括：
boolean hasNext(): 判断集合是否还有下一个元素。
E next(): 返回集合中的下一个元素。
void remove(): 从集合中移除当前迭代的元素（可选操作）。

### Iterable 接口:

Iterable 接口是所有实现了 foreach 循环的类的父接口。
集合类实现了 Iterable 接口。

#### 主要方法是：
Iterator<E> iterator(): 返回一个用于迭代集合中元素的迭代器。

### Concurrent 接口:

java.util.concurrent 包中的接口和类提供了并发编程的支持，如 BlockingQueue。
