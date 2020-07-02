# Java基础
### 1.ConcurrentHashmap为什么是线程安全的：
在底层put等方法插入时应用Synchronize关键字，在添加元素时候，采用synchronized来保证线程安全，然后计算size的时候采用CAS操作进行计算。
### 2.线程方法：
yield() 线程让步
