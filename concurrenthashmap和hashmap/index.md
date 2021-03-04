# ConcurrentHashMap是如何保证线程安全的



### 参考 [ConcurrentHashMap是如何保证线程安全的](https://www.cnblogs.com/jing99/p/11330341.html)

#### [HashMap和HashTable的区别](https://crossoverjie.top/2018/07/23/java-senior/ConcurrentHashMap/)

- HashTable 是非常高效率的数据结构，但HashMap和HashTable在线程的环境下使用并不合理
- HashMap: HashMap是线程不安全的，在并发环境下，可能会形成环状链表（扩容时可能造成，具体原因自行百度google或查看源码分析），导致get操作时，cpu空转，所以，在并发环境中使用HashMap是非常危险的。
- HashTable:HashTable和HashMap的实现原理几乎一样，差别无非是1.HashTable不允许key和value为null；2.HashTable是线程安全的。但是HashTable线程安全的策略实现代价却太大了，简单粗暴，get/put所有相关操作都是synchronized的，这相当于给整个哈希表加了一把大锁，多线程访问时候，只要有一个线程访问或操作该对象，那其他线程只能阻塞，相当于将所有的操作串行化，在竞争激烈的并发场景中性能就会非常差。

![HashTable](https://images2015.cnblogs.com/blog/1024555/201705/1024555-20170514173954488-1353945142.png)

#### 使用ConcurrentHashMap解决全段锁的问题 

![ConcurrentHashMap](https://images2015.cnblogs.com/blog/1024555/201705/1024555-20170514174100832-1891630860.png)


- 和 HashMap 非常类似，唯一的区别就是其中的核心数据如 value ，以及链表都是 volatile 修饰的，保证了获取时的可见性。 
- 原理上来说：ConcurrentHashMap 采用了分段锁技术，其中 Segment 继承于 ReentrantLock。不会像 HashTable 那样不管是 put 还是 get 操作都需要做同步处理，理论上 ConcurrentHashMap 支持 CurrencyLevel (Segment 数组数量)的线程并发。每当一个线程占用锁访问一个 Segment 时，不会影响到其他的 Segment。

#### 1.7


如何实现呢？这就用到了ConcurrentHashMap中最关键的Segment。
ConcurrentHashMap中维护着一个Segment数组，每个Segment可以看做是一个HashMap。
而Segment本身继承了ReentrantLock，它本身就是一个锁。
在Segment中通过HashEntry数组来维护其内部的hash表。
每个HashEntry就代表了map中的一个K-V，用HashEntry可以组成一个链表结构，通过next字段引用到其下一个元素。

![](https://i.loli.net/2019/05/08/5cd1d2c5ce95c.jpg)
##### PUT的流程

- 将当前 Segment 中的 table 通过 key 的 hashcode 定位到 HashEntry。
- 遍历该 HashEntry，如果不为空则判断传入的 key 和当前遍历的 key 是否相等，相等则覆盖旧的 value。
- 不为空则需要新建一个 HashEntry 并加入到 Segment 中，同时会先判断是否需要扩容。
- 最后会解除在 1 中所获取当前 Segment 的锁。

##### GET的流程

- 只需要将 Key 通过 Hash 之后定位到具体的 Segment ，再通过一次 Hash 定位到具体的元素上。
- 由于 HashEntry 中的 value 属性是用 volatile 关键词修饰的，保证了内存可见性，所以每次获取时都是最新值。
- ConcurrentHashMap 的 get 方法是非常高效的，因为整个过程都不需要加锁。

#### 1.8

![](https://i.loli.net/2019/05/08/5cd1d2ce33795.jpg)
其中抛弃了原有的 Segment 分段锁，而采用了 CAS + synchronized 来保证并发安全性。


##### PUT的流程

- 根据 key 计算出 hashcode。
- 判断是否需要进行初始化。
- f 即为当前 key 定位出的 Node，如果为空表示当前位置可以写入数据，利用 CAS 尝试写入，失败则自旋保证成功。
- 如果当前位置的 hashcode == MOVED == -1,则需要进行扩容。
- 如果都不满足，则利用 synchronized 锁写入数据。
- 如果数量大于 TREEIFY_THRESHOLD 则要转换为红黑树。

##### GET的流程

- 根据计算出来的 hashcode 寻址，如果就在桶上那么直接返回值。
- 如果是红黑树那就按照树的方式获取值，若不满足那就按照链表的方式遍历获取值。








#### 常见关于 HashMap || ConcurrentHashMap 的问题整理

1. 谈谈你理解的 HashMap，讲讲其中的 get put 过程。
2. 1.8 做了什么优化？
3. 是线程安全的嘛？
4. 不安全会导致哪些问题？
5. 如何解决？有没有线程安全的并发容器？
6. ConcurrentHashMap 是如何实现的？ 1.7、1.8 实现有何不同？为什么这么做？


