Synchronized ----> wait, notifyl), notifyAll()
![截屏2024-02-13 15.47.20.png](https://img.xwyue.com/i/2024/02/13/65cb8f8ec4930.png)

synchronized的几种用法，包括在方法上和方法内部使用   
• synchronized关键字。    
对于静态方法和普通方法，使用synchronized关键字会阻塞线程，而对于同步代码块，需要指定需要锁定的对象。此外，还介绍了锁定this 和class的区别。在开发中，使用同步代码块来锁定共享对象是常见的，而使用this 和class的方式相对较少，但仍需注意其作用域的不同。   
• synchronized的多种用法,包括锁定静态方法和普通方法、锁定静态对象和非静态对象等。    
同步方法的调用：讲解了同步方法的调用，以及静态方法和普通方法的区别。    
同步代码块的用法：介绍了同步代码块的用，以及如何指定需要锁定的对象。   
锁定对象的方式：讲解了锁定对象的方式，包括this和class的区别。   

在Java中，有三种主要的使用 synchronized 的语法：

Synchronized 方法:

通过在方法的声明中使用 synchronized 关键字，可以将整个方法标记为同步方法。这意味着在任何时刻只有一个线程可以执行该方法。
```code
public synchronized void synchronizedMethod() {
    // 代码块
}

```

Synchronized 代码块:

使用 synchronized 关键字创建一个同步代码块，将需要同步的代码包裹在这个块中。这样可以实现更细粒度的同步，而不是整个方法。     
```code

public void someMethod() {
    // 非同步代码
    synchronized (lockObject) {
        // 需要同步的代码块
    }
    // 非同步代码
}
```

在这里，lockObject 可以是任何对象，它将被用作锁。   

Synchronized 静态方法:     

对于静态方法，可以使用 synchronized 关键字来标记整个静态方法，实现对静态方法的同步控制。     
  
```code
public static synchronized void synchronizedStaticMethod() {
    // 代码块
}
```


wait() & notify(), notifyAll()      
在多线程编程中，wait 方法是让当前线程进入休眠状态，直到另一个线程调用了notify 或notity All 方法之后，才能继续恢复执行。而在 Java中，wait 和notity/notifyAll 有着一套自己的使用格式要求，也就是在使用 wait 和 notity(notifyAll 的使用和 notity 类似，所以下文就只用 notify 用来指代二者)必须配合synchronized 一起使用才行。          
无论是 wait 还是notity，如果不配合 synchronized一起使用，在程序运行时就会报illegalMonitorState Exception 非法的监视器状态异常，而且 notity 也不能实现程序的唤醒功能了。    


