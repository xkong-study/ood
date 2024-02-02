![1706873898066.png](https://img.xwyue.com/i/2024/02/02/65bcd42c7a3c4.png)

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
HashSet

LinkedHashSet
add(E element): 将指定元素添加到集合中。
remove(Object element): 删除指定元素。
contains(Object element): 判断集合是否包含指定元素。
clear(): 清空集合中的所有元素。
iterator(): 返回集合的迭代器。

TreeSet

### Queue 接口:
Queue 接口主要用于表示队列行为，而队列操作通常包括在队尾添加元素和在队头移除元素。push 和 pop 方法更常用于栈的操作。为了保持接口的简洁性和语义的清晰性，Queue 接口没有包含这两个方法。如果需要同时支持队列和栈的操作，可以使用 Deque 接口。

Queue 接口表示一个队列，支持在队尾添加元素，队头移除元素。
子接口包括 Deque。
常见实现类有 LinkedList、PriorityQueue。

添加元素：
boolean add(E element): 将指定的元素添加到队列尾部，如果队列已满则抛出异常。
boolean offer(E element): 将指定的元素添加到队列尾部，如果队列已满则返回 false。

移除元素：
E remove(): 移除并返回队列头部的元素，如果队列为空则抛出异常。
E poll(): 移除并返回队列头部的元素，如果队列为空则返回 null。

获取元素：
E element(): 返回队列头部的元素，但不移除，如果队列为空则抛出异常。
E peek(): 返回队列头部的元素，但不移除，如果队列为空则返回 null。

其他方法：
boolean isEmpty(): 判断队列是否为空。
int size(): 返回队列中的元素个数。
boolean contains(Object element): 判断队列是否包含指定的元素。
Iterator<E> iterator(): 返回队列的迭代器。


### Deque 接口:

Deque 接口是一个双端队列，支持在两端进行元素的插入和删除操作。
常见实现类有 LinkedList、ArrayDeque。

是的，在一般的队列实现中，push 和 pop 操作通常与栈相关，会在队列的尾部执行。这是因为栈的特点是"先进后出"（Last In, First Out，LIFO），新元素被推入栈的顶部，而弹出元素也发生在顶部。

在单纯的队列（不是双端队列）中，一般使用 offer（或 enqueue）在队尾添加元素，使用 poll（或 dequeue）从队头移除元素。这是典型的"先进先出"（First In, First Out，FIFO）行为，新元素被添加到队列的尾部，而移除元素则发生在队列的头部。

因此，push 和 pop 这两个术语一般在栈的上下文中使用，表示在栈顶执行添加和移除操作。在队列中，更常见的术语是 offer、poll 等。在双端队列（Deque）中，由于支持两端操作，push 和 pop 可能发生在队头或队尾，具体取决于实际使用的方法和实现。

### Map 接口:

Map 接口表示键值对的映射。
常见实现类有 HashMap、LinkedHashMap、TreeMap。

LinkedHashMap常用方法：

put(K key, V value): 将指定的键值对添加到映射表中。
get(Object key): 返回指定键对应的值。
remove(Object key): 删除指定键对应的映射。
clear(): 清空映射表中的所有映射。
entrySet(): 返回映射表中的所有映射条目。

### SortedMap 接口:

SortedMap 接口继承自 Map 接口，表示一个按键进行排序的映射。
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
