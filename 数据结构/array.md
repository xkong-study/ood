### 数组（Array）是一种线性表数据结构。它用一组连续的内存空间，来存储一组具有相同类型的数据。

1.线性表数据结构：
线性表就是数据排成像一条线一样的结构。每个线性表上的数据最多只有前和后两个方向。其实除了数组，链表、队列、栈等也是线性表结构。

我们知道，计算机会给每个内存单元分配一个地址，计算机通过地址来访问内存中的数据。当计算机需要随机访问数组中的某个元素时，它会首先通过下面的寻址公式，计算出该元素存储的内存地址：

a[i]_address = base_address + i * data_type_size

其中 data_type_size 表示数组中每个元素的大小。我们举的这个例子里，数组中存储的是 int 类型数据，所以 data_type_size 就为 4 个字节。

将元素索引 i 乘以每个元素的大小 data_type_size，然后加上数组的起始地址 base_address，可以得到数组中第 i 个元素的内存地址。

在面试的时候，常常会问数组和链表的区别，很多人都回答说，“链表适合插入、删除，时间复杂度 O(1)；数组适合查找，查找时间复杂度为 O(1)”。
实际上，这种表述是不准确的。数组是适合查找操作，但是查找的时间复杂度并不为 O(1)。即便是排好序的数组，你用二分查找，时间复杂度也是 O(logn)。所以，正确的表述应该是，数组支持随机访问，根据下标随机访问的时间复杂度为 O(1)。

### 为什么数组要从 0 开始编号，而不是从 1 开始？
从数组存储的内存模型上来看，“下标”最确切的定义应该是“偏移（offset）”。前面也讲到，如果用 a 来表示数组的首地址，a[0]就是偏移为 0 的位置，也就是首地址，a[k]就表示偏移 k 个 type_size 的位置，所以计算 a[k]的内存地址只需要用这个公式：

address = base_address + k * type_size

但是，如果数组从 1 开始计数，那我们计算数组元素 a[k]的内存地址就会变为：

a[k]_address = base_address + (k-1)*type_size

对比两个公式，我们不难发现，从 1 开始编号，每次随机访问数组元素都多了一次减法运算，对于 CPU 来说，就是多了一次减法指令。

数组作为非常基础的数据结构，通过下标随机访问数组元素又是其非常基础的编程操作，效率的优化就要尽可能做到极致。所以为了减少一次减法操作，数组选择了从 0 开始编号，而不是从 1 开始。

### ood
```
class CustomArray {
  constructor() {
    this.elements = [];
  }

  // 添加元素到数组
  push(data) {
    const index = this.elements.length;
    this.elements.push({ index, data });
  }

  // 获取数组长度
  get length() {
    return this.elements.length;
  }

  // 获取数组中的元素对象
  get(index) {
    if (index < 0 || index >= this.elements.length) {
      throw new Error("Index out of bounds");
    }
    return this.elements[index];
  }

  // 删除数组中的元素
  delete(index) {
    if (index < 0 || index >= this.elements.length) {
      throw new Error("Index out of bounds");
    }
    const deletedElement = this.elements.splice(index, 1)[0];
    return deletedElement.data;
  }

  // 在指定位置插入元素
  insert(index, data) {
    if (index < 0 || index > this.elements.length) {
      throw new Error("Index out of bounds");
    }
    this.elements.splice(index, 0, { index, data });
  }

  // 遍历数组
  forEach(callback) {
    this.elements.forEach(callback);
  }
}
```
##### asList(T... a)
将指定数组转换为 List。
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

##### binarySearch(T[] a, T key)
在指定的数组中使用二分查找算法搜索指定的元素。

##### copyOf(T[] original, int newLength)
复制指定的数组，截取或填充零（或 null）以获得所需的长度。

##### equals(T[] a, T[] a2)
比较两个数组是否相等。

##### fill(T[] a, T val)
将数组的所有元素替换为指定的值。

##### sort(T[] a)
对数组进行排序。
toString(T[] a)
返回包含数组元素的字符串表示形式。

##### deepEquals(Object[] a1, Object[] a2)
递归地比较两个数组，如果两个数组包含相同的元素，则返回 true。

##### deepToString(Object[] a)
返回包含数组元素的深层字符串表示形式。

##### hashCode(T[] a)
返回数组的哈希码。

##### copyOfRange(T[] original, int from, int to)
复制指定范围的数组。

##### fill(T[] a, int fromIndex, int toIndex, T val)
将数组的指定范围内的元素替换为指定的值。

##### sort(T[] a, Comparator<? super T> c)

Integer[] numbers = {5, 2, 9, 1, 5, 6};
Arrays.sort(numbers);
使用指定的比较器对数组进行排序。

#####parallelSort(T[] a)

使用并行排序算法对数组进行排序。

