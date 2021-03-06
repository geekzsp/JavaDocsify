# JAVA IO

!> 同步和异步关注的是**消息通信机制**

* 同步：在发出一个调用时，在没有得到结果之前，该调用就不返回。但是一旦调用返回，就得到返回值了。
* 异步：调用发出之后，这个调用就直接返回了，所以没有返回结果

!> 阻塞和非阻塞：程序在**等待调用结果时的状态。**

* 阻塞调用是指调用结果返回之前，当前线程会被挂起。调用线程只有在得到结果之后才会返回。
* 非阻塞调用指在不能立刻得到结果之前，该调用不会阻塞当前线程。
* IO 分类
  * BIO(Block-IO)阻塞IO
  * NIO(Non-Block-IO)非阻塞IO
  * AIO(Asynchronous I/O)异步非阻塞IO
* NIO和IO的区别
  1. IO是面向流的 NIO是面向缓存区的
  2. IO流是阻塞的 NIO流是非阻塞的
  3. NIO有选择器  IO没有



