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
