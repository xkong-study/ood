## 引用类型要初始化

对于引用类型，Java会给它们分配默认值 null，但是如果你想要使用这个引用类型的对象，你需要显式地进行初始化。这可以通过使用 new 关键字来创建对象或者调用构造函数进行初始化。

例如，如果你有一个 ArrayList 类型的引用变量，你需要在使用它之前创建一个实际的 ArrayList 对象：

ArrayList<Integer> list = new ArrayList<Integer>(); // 创建并初始化 ArrayList 对象    

如果你忘记初始化引用变量，试图使用未初始化的引用变量将导致 NullPointerException。因此，确保在使用引用类型之前对它们进行初始化是很重要的。
