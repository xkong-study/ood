semaphore

![截屏2024-02-13 17.07.50.png](https://img.xwyue.com/i/2024/02/14/65cba218f3176.png)

![截屏2024-02-13 17.10.50.png](https://img.xwyue.com/i/2024/02/14/65cba3380edcb.png)

1188 超出时间限制
```code
class BoundedBlockingQueue {
    Semaphore enqueue;
    Semaphore dequeue;
    int size;
    Queue<Integer> queue = new LinkedList<>();
    public BoundedBlockingQueue(int capacity) {
     enqueue = new Semaphore(capacity);
     dequeue = new Semaphore(0);
     this.size = capacity;
    }
    
    public synchronized void enqueue(int element) throws InterruptedException {
     enqueue.acquire();
     queue.offer(element);
     dequeue.release();
    }
    
    public synchronized int dequeue() throws InterruptedException {
    dequeue.acquire();
    int ans = queue.poll();
    enqueue.release();
    return ans;
    }
    
    public synchronized int size() {
     return queue.size();   
    }
}
```
在这个代码中，acquire 是 Semaphore 类中的方法，用于获取信号量。Semaphore 是一个计数信号量，维护了一个可用的许可数。acquire 方法的作用是获取一个许可，如果当前可用许可数为0，则该线程将阻塞，直到有可用许可。    

具体到你的实现，这里有两个 Semaphore 对象，enqueue 和 dequeue，它们分别用于控制队列的入队和出队操作。让我们来解释一下它们在你的代码中的作用：    

enqueue Semaphore：在构造函数中，通过 enqueue = new Semaphore(capacity) 初始化，表示队列的容量。在 enqueue 操作中，enqueue.acquire() 将阻塞线程，直到有可用的许可。每当有一个元素被入队时，许可数减少，当队列达到容量时，后续的 enqueue 操作将被阻塞。   

dequeue Semaphore：在构造函数中，通过 dequeue = new Semaphore(0) 初始化，表示初始时队列为空。在 dequeue 操作中，dequeue.acquire() 将阻塞线程，直到有元素可供出队。每当一个元素被出队时，许可数增加，当队列为空时，后续的 dequeue 操作将被阻塞。   

这样，通过这两个 Semaphore 对象的配合，实现了对队列的入队和出队操作的同步和限制，确保在正确的时机进行操作，防止队列溢出或下溢。  
