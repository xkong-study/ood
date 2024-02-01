队列是一种先进先出 (FIFO)的、线性的数据结构，与栈的结构类似，只是最先入队到队列的数据，会第一个出队，这与栈相反。

常见的应用场景是基于事件的处理系统

1.比如js的事件处理机制
2.订单处理系统
3.邮件处理系统

都是基于消息队列实现的

queue的class：
1.enqueue

```
class queue{
const items = []
enqueue(item){
this.items.push(item)
}
dequeue{
if(this.isEmpty()){
return "queue is empty";
}
return this.items.shift();
}
isEmpty(){
this.size() == 0;
}
size(){
return this.items.length;
}
front()
{
this.items[0];
}
}
```
this 关键字是一个非常重要的概念。它通常被用来指代当前对象的实例。所以当你在一个类的方法内使用 this 时，你实际上是在引用当前实例的其他属性或者方法。
