ArrayList 类实现了 List 接口，因此包括了 List 接口中定义的一系列方法。以下是 ArrayList 类的一些常用方法：

基本操作：

boolean add(E e): 将指定的元素添加到列表的末尾。
void add(int index, E element): 在指定位置插入指定元素。
boolean addAll(Collection<? extends E> c): 将指定 collection 中的所有元素添加到列表的末尾，按照指定 collection 的迭代器返回这些元素的顺序。
boolean addAll(int index, Collection<? extends E> c): 将指定 collection 中的所有元素插入到列表中，从指定的位置开始。
void clear(): 从列表中移除所有元素。
boolean remove(Object o): 从列表中移除指定元素的第一个匹配项。
E remove(int index): 移除列表中指定位置的元素。
boolean removeAll(Collection<?> c): 从列表中移除包含在指定 collection 中的所有元素。
检索元素：

E get(int index): 返回列表中指定位置的元素。
int indexOf(Object o): 返回指定元素在列表中第一次出现的索引，如果不存在则返回 -1。
int lastIndexOf(Object o): 返回指定元素在列表中最后一次出现的索引，如果不存在则返回 -1.
修改和替换：

E set(int index, E element): 用指定的元素替代列表中指定位置的元素。
子列表：

List<E> subList(int fromIndex, int toIndex): 返回列表中指定的 fromIndex（包括）和 toIndex（不包括）之间的部分视图。
其他：

boolean contains(Object o): 如果列表包含指定的元素，则返回 true。
int size(): 返回列表中的元素数。
boolean isEmpty(): 如果列表不包含元素，则返回 true。
Object[] toArray(): 将列表转换为数组。
numbers.removeIf(number -> number == valueToRemove);
