volatile
![截屏2024-02-14 00.35.00.png](https://img.xwyue.com/i/2024/02/14/65cc0c6188d3f.png)

缓存一致性协议     
刚才我在说可见性的时候，说"如果一个共享变量被一个线程修改了之后，当其他线程要读取这个变量的时候，最终会去内存中读取，而不是从自己的工作空间中读取"，实际上是这样的：    
线程中的处理器会一直在总线上嗅探其内部缓存中的内存地址在其他处理器的操作情况，一旦嗅探到某处处理器打算修改其内存地址中的值，而该内存地址刚好也在自己的内部缓存中，那么处理器就会强制让自己对该缓存地址的无效。所以当该处理器要访问该数据的时候，由于发现自己缓存的数据无效了，就会去主存中访问。    


volatile可以使得变量强制 保存在主内存sharedmemory中。两个线程都可以同时读取到    

![截屏2024-02-14 10.50.19.png](https://img.xwyue.com/i/2024/02/14/65cc9be83c135.png)

![截屏2024-02-14 10.55.02.png](https://img.xwyue.com/i/2024/02/14/65cc9cbe70f52.png)

![截屏2024-02-14 11.00.52.png](https://img.xwyue.com/i/2024/02/14/65cc9da7225c4.png)

不能写a=a+b

线程不安全，不建议使用。只是变成了shared variable类似     

