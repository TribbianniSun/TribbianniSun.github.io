# 简述TCP的time_wait摘抄



["简述TCP的time_wait摘抄"](https://yuerblog.cc/2020/03/09/%E5%85%B3%E4%BA%8Etime_wait%E9%97%AE%E9%A2%98%E7%AE%80%E8%BF%B0%E4%B8%8E%E4%BC%98%E5%8C%96/)
<!--more-->



## 什么是 TIME_WAIT
主动关闭连接的一方最终进入TIME_WAIT状态等待一段才真正的释放内核中的连接记录，在释放记录之前这个连接使用的本地端口将一直被占用。

保持一段时间的TIME_WAIT的理由是：担心”ack N+1″没有送达，导致被动方重传”FIN N”，那么主动方应当再次响应”ack N+1″。

如果没有TIME_WAIT就直接复用该连接占用的端口，那么万一被动方重传”FIN N”，那么使用相同端口的新连接就会被错误关闭。

![](https://yuerblog.cc/wp-content/uploads/2020/03/1-1.jpg)

## 优化TIME_WAIT

- 谁主动关闭socket，谁TIME_WAIT。
- 如果双方响应正常，TIME_WAIT应该只是瞬间状态。

因此，不明确”客户端主动关闭”/”服务端主动关闭”就讨论TIME_WAIT就是耍流氓。


## 服务端主动关闭

无论有多少连接，服务端都只有一个端口，那就是监听端口，大量连接之间的差异仅仅是TCP 4元祖的客户端ip和port不同而已。

因此服务端TIME_WAIT压根不会耗尽端口，因为它就一个端口。

那么服务端就不需要优化了吗？对，没必要优化，一个TIME_WAIT的4元祖当遇到新的SYN时会复用，不需要特殊配置。

另外，当TIME_WAIT数量超过内核选项net.ipv4.tcp_max_tw_buckets的限制时，多余的TIME_WAIT连接将被立即关闭，然后在netstat -s中留下如下的溢出统计指标：

TCPTimeWaitOverflow: 127688100


## 客户端主动关闭
客户端每个连接都会随机选择一个本地端口，所以最终会导致客户端大量端口处于TIME_WAIT状态，这和服务端主动关闭是最大的不同。

所以我们通常所说的TIME_WAIT问题都是针对客户端的，只是好像很少有人提及这一点。

网上有一种优化手段是把net.ipv4.tcp_max_tw_buckets调低，这样TIME_WAIT连接就会被删除，但是这不是一个最佳手段哈。


目前唯一安全的选项就是同时开启如下2个选项：

- net.ipv4.tcp_timestamps=1（连接发起方和接收方都需要开启）
- net.ipv4.tcp_tw_reuse=1（只影响连接发起方）

它的作用是向外发起连接的时候，可以复用TIME_WAIT的端口，但是有一个前提：

该端口最后一次通讯时间距离当前系统时间>1秒



tcp timestamp选项的作用就是内核会记录端口的最后通讯时间，这样reuse选项才有判断依据。

那么客户端复用TIME_WAIT连接，对服务端有啥影响呢？


TIME_WAIT就是为了确保给被动方的FIN回复ACK成功，这样对方才会离开LAST-ACK彻底结束连接。

图中的叉号就是回复ACK丢失的情况，按道理应该继续TIME_WAIT等待被动关闭方重传FIN，然而我们这时候我们重用端口新建到服务端的连接，发送SYN会被对方忽略，因为对方还处在上一个连接的LAST-ACK状态。

被动方稍后重传FIN，客户端的端口已经是SYN-SENT新建连接状态，因此回复对方RST让对方退出LAST-ACK状态。此后，客户端重传SYN，被动关闭方正常回复SYN+ACK，连接建立完成。

看起来，唯一顾虑的就是SYN重传会不会导致连接变慢？可能需要实际测试测试。

另外还有2个辅助优化手段，就是扩大内核选择端口的范围，比如调大为：

net.ipv4.ip_local_port_range = 5120 65000

还有降低TIME_WAIT的保持时间（可以更短，比如10秒）：

net.ipv4.tcp_fin_timeout=30

这样客户端可以有更多的端口使用。



## 总结
在所有机器上，生效如下参数：

net.ipv4.tcp_timestamps=1
net.ipv4.tcp_tw_reuse=1
net.ipv4.ip_local_port_range = 5120 65000
net.ipv4.tcp_fin_timeout=30
如果你的内核版本低，那么需要确保禁用掉一个垃圾选项，它已经在4.x内核里彻底删除了：

net.ipv4.tcp_tw_recycle=0
这可以应对TIME_WAIT问题，但是不是解决短连接问题的所有参数（可以阅读我的上一篇关于K8S的博客）。



