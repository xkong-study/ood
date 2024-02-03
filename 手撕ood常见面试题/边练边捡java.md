## 基本数据类型
基本数据类型byte short int long float double char boolean
基本数据类型都是没有属性和方法的 要变成包装类才会有方法

## 基本数据类型的包装类
### Integer：

parseInt(String s): 将字符串转换为整数。
valueOf(int i): 返回一个表示指定整数值的 Integer 实例。
compareTo(Integer anotherInteger): 比较两个整数。
toString(): 将整数转换为字符串。

### Long：

parseLong(String s): 将字符串转换为长整数。
valueOf(long l): 返回一个表示指定长整数值的 Long 实例。
compareTo(Long anotherLong): 比较两个长整数。
toString(): 将长整数转换为字符串。

### Short：

parseShort(String s): 将字符串转换为短整数。
valueOf(short s): 返回一个表示指定短整数值的 Short 实例。
compareTo(Short anotherShort): 比较两个短整数。
toString(): 将短整数转换为字符串。

### Byte：

parseByte(String s): 将字符串转换为字节。
valueOf(byte b): 返回一个表示指定字节值的 Byte 实例。
compareTo(Byte anotherByte): 比较两个字节。
toString(): 将字节转换为字符串。

### Double：

parseDouble(String s): 将字符串转换为双精度浮点数。
valueOf(double d): 返回一个表示指定双精度浮点数值的 Double 实例。
compareTo(Double anotherDouble): 比较两个双精度浮点数。
toString(): 将双精度浮点数转换为字符串。

### Float：

parseFloat(String s): 将字符串转换为单精度浮点数。
valueOf(float f): 返回一个表示指定单精度浮点数值的 Float 实例。
compareTo(Float anotherFloat): 比较两个单精度浮点数。
toString(): 将单精度浮点数转换为字符串。

### Character：

isDigit(char ch): 判断字符是否是数字。
isLetter(char ch): 判断字符是否是字母。
toUpperCase(char ch): 将字符转换为大写。
toLowerCase(char ch): 将字符转换为小写。

### Boolean：

parseBoolean(String s): 将字符串转换为布尔值。
valueOf(boolean b): 返回一个表示指定布尔值的 Boolean 实例。
compareTo(Boolean anotherBoolean): 比较两个布尔值。
toString(): 将布尔值转换为字符串。

### ==：
1.比较常量，基本数据类型会自动转变类型进行比较
2.比较对象，会比较对象是否引用同一个地址

```code
String str1 = new String("hello");
String str2 = new String("hello");

str1 = str1.intern();  // 将str1放入常量池
str2 = str2.intern();  // 将str2放入常量池

System.out.println(str1 == str2);  // true，str1 和 str2 引用相同的对象（都在常量池中）
```
### ===：
1.比较值和类型是否都相等。

### 比较字符串应该使用 equals 

### 如何使用length
基本数据类型：     

int, short, long, byte, char, float, double, boolean：这些都是基本数据类型，没有 length 属性。     
数组（Array）：    
    
数组是一种对象，但它有一个名为 length 的属性，用于表示数组的长度。    
int[] intArray = {1, 2, 3, 4, 5};     
int arrayLength = intArray.length;     
字符串（String）：     
     
字符串是一个对象，有一个 length() 方法，用于获取字符串的字符数。     
String str = "Hello, Java!";     
int strLength = str.length();     
集合框架中的对象（如 List、Queue）：      

针对集合框架中的对象，通常使用 size() 方法来获取元素的数量。     
List<String> stringList = new ArrayList<>();      
int listSize = stringList.size();      

队列（Queue）：       
 
对于标准的 Java 队列实现，例如 LinkedList 或 ArrayDeque，也是使用 size() 方法。      

Queue<Integer> queue = new LinkedList<>();      
int queueSize = queue.size();      

总体而言，对于数组使用 length，对于字符串使用 length()，对于集合框架中的对象使用 size()。这是 Java 中常见的长度或大小表示方法。     
