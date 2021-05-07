# Sleep和wait的区别摘抄



[Sleep和wait的区别摘抄](https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/multi-thread/2020%E6%9C%80%E6%96%B0Java%E5%B9%B6%E5%8F%91%E5%9F%BA%E7%A1%80%E5%B8%B8%E8%A7%81%E9%9D%A2%E8%AF%95%E9%A2%98%E6%80%BB%E7%BB%93.md#9-%E8%AF%B4%E8%AF%B4-sleep-%E6%96%B9%E6%B3%95%E5%92%8C-wait-%E6%96%B9%E6%B3%95%E5%8C%BA%E5%88%AB%E5%92%8C%E5%85%B1%E5%90%8C%E7%82%B9)
<!--more-->


## sleep 和 wait的区别
- 两者最主要的区别在于：sleep() 方法没有释放锁，而 wait() 方法释放了锁 。
- 两者都可以暂停线程的执行。
- wait() 通常被用于线程间交互/通信，sleep() 通常被用于暂停执行。
- wait() 方法被调用后，线程不会自动苏醒，需要别的线程调用同一个对象上的 notify() 或者 notifyAll() 方法。sleep() 方法执行完成后，线程会自动苏醒。或者可以使用 wait(long timeout) 超时后线程会自动苏醒。


