# java

## HashMap

### Java 中 HashMap 的存储, 冲突, 扩容, 并发访问分别是怎么解决的

拉链法（长度大于8变形为红黑树）,扩容*2 rehash，并发访问不安全

### 为什么到8变红黑树

到8的概率低，维护树需要成本

### 为什么不用avl树

插删成本更低

### ConcurrentHashMap

1.7：分段锁每段各为一个hashmap，两次哈希到达最终位置
1.8：在hashmap基础上改进。只锁节点即可
[ConcurrentHashMap](https://www.cnblogs.com/yangming1996/p/8031199.html "https://www.cnblogs.com/yangming1996/p/8031199.html")

## 个人没怎么用过的奇怪Collection/Map

CopyOnWriteArrayList 每次插入都复制整个数组，写完后将指针指向新数组。是线程安全的

Vector 线程安全，以synchronized保证线程安全，性能弱于楼上

ConcurrentSkipListMap 跳表实现的Map



## Java内存模型

### 几个性质

1. 原子性：保证 Java内存模型中原子变量内存操作的。通常有 read、write、load、use、assign、store、lock、unlock等这些。

2. 可见性：就是当一个线程对一个变量进行了修改，其他线程即可立即得到这个变量最新的修改数据。

3. 有序性：如果在本线程内观察，所有操作都是有序的；如果在一个线程中观察另一个线程，所有操作都是无序的。（重排序）

4. 先行发生：happen-before 先行发生原则是指Java内存模型中定义的两项操作之间的依序关系，如果说操作A先行发生于操作B，其实就是说发生操作B之前.

5. 传递性

  ### 通信

  通信 是指线程之间以何种机制来交换信息。在命令式编程中，线程之间的通信机制有两种：共享内存 和 消息传递。

在共享内存的并发模型里，线程之间共享程序的公共状态，线程之间通过写-读内存中的公共状态来隐式进行通信。

在消息传递的并发模型里，线程之间没有公共状态，线程之间必须通过明确的发送消息来显式进行通信。

## JVM垃圾回收机制

### 三种算法

标记清除法

引用计数

复制算法

### 内存划分

新生代1/3

eden 8/10
survivor0 1/10
survivor1 1/10

### 为什么GC需要stw

防止过程中产生新的引用导致错误的回收

### CMS

[CMS](https://www.jianshu.com/p/08f0b85ad665)

### G1

[G1](https://blog.csdn.net/coderlius/article/details/79272773 "https://blog.csdn.net/coderlius/article/details/79272773")

### GC ROOT

一个对象可以属于多个root，GC root有几下种：

Class - 由系统类加载器(system class loader)加载的对象，这些类是不能够被回收的，他们可以以静态字段的方式保存持有其它对象。我们需要注意的一点就是，通过用户自定义的类加载器加载的类，除非相应的java.lang.Class实例以其它的某种（或多种）方式成为roots，否则它们并不是roots，.

Thread - 活着的线程

Stack Local - Java方法的local变量或参数

JNI Local - JNI方法的local变量或参数

JNI Global - 全局JNI引用

Monitor Used - 用于同步的监控对象

Held by JVM - 用于JVM特殊目的由GC保留的对象，但实际上这个与JVM的实现是有关的。可能已知的一些类型是：系统类加载器、一些JVM知道的重要的异常类、一些用于处理异常的预分配对象以及一些自定义的类加载器等。然而，JVM并没有为这些对象提供其它的信息，因此需要去确定哪些是属于"JVM持有"的了。

## 双亲委派模型

双亲委派模型：如果一个类加载器收到了类加载的请求，它首先不会自己去加载这个类，而是把这个请求委派给父类加载器去完成，每一层的类加载器都是如此，这样所有的加载请求都会被传送到顶层的启动类加载器中，只有当父加载无法完成加载请求（它的搜索范围中没找到所需的类）时，子加载器才会尝试去加载类。

## FULL GC频繁触发原因查询

1. 内存中加载的数据量过于庞大，如一次从数据库取出过多数据；
2. 集合类中有对对象的引用，使用完后未清空，使得JVM不能回收；
3. 代码中存在死循环或循环产生过多重复的对象实体；
4. 使用的第三方软件中的BUG；
5. 启动参数内存值设定的过小；

[线上FullGC频繁的排查](https://blog.csdn.net/wilsonpeng3/article/details/70064336)



## 乐观锁 悲观锁 自旋锁 cas

### 悲观锁

同一时刻只允许一个线程进行操作

### 乐观锁

读取不加锁，写入时判断是否有更改。脏数据的读取是必然的

#### 两种实现

version：每次更新时version+1，读取时一并取出version。如果更新时发现version与已获得version不一致，则更新失败。

CAS：



## 多线程

### sleep()和wait()

sleep方法是Thread类的静态方法,wait()是Object超类的成员方法

sleep不会释放锁，wait会释放



## 杂项

### Math.floor和强制转换有啥区别

正数一样，但负数强转是返回比较大的。

## java面试题

偏简单：[java面试题](https://www.zhihu.com/question/27858692/answer/787505434?hb_wx_block=1&utm_source=wechat_session&utm_medium=social&utm_oi=805956537267912704)

​	[使用序列化进行java对象深拷贝](https://mp.weixin.qq.com/s/w1s1PbsHrZEU7e04pUkDOg)



