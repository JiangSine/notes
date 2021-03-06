
## IO的工作机制
---

* 基于字节操作的IO
* 基于字符操作的IO
* 基于磁盘操作的IO

#### 基于字节的操作
InputStream、OutputStream.

1. 操作数据的方式是可以组合使用的。
```
OutputStream outputStream = new BufferedOutPutStream(new ObjectOutputStream(new FileOutPutStream("file")));
```
2. 必须要指定要写到那里去。
#### 基于字符的操作
定义了如何读写，不关心读写到哪里去。

##### 字节与字符之间的转化
InputStreamReader、OutputStreamWriter是字符和字节之间的桥梁。


##### 磁盘IO 工作机制
1. 标准访问文件：用户调用系统接口write()之后，application将数据从用户地址空间复制到内核用户空间之后，对于用户而言，写操作已经完成。
至于何时写到磁盘，由操作系统决定。
2. 直接IO方式：application直接与磁盘交互。这样有好处，也有坏处。如果application可以做一些缓存处理，或者将热点数据加载到内存，就会加快访问效率。
但是如果，没有缓存，每次都从磁盘加载，则会很慢。
3. 同步访问文件：数据的读和写都是同步操作的，只有成功写入到磁盘才会返回成功。
4. 异步访问文件：
5. 内存映射：操作系统将内存中的一块区域与磁盘中的文件关联起来。



#### IO调优
磁盘优化，增加缓存，底层优化（RAID,操作系统优化）。
TCP参数优化

网络IO优化
1. 减少网络交互
2. 减少数据量的大小。

同步和异步：一个任务依赖另一个任务，只有等待被依赖的任务完成时，任务才完成，就是同步。异步就是只要本身任务完成，就算完成。
阻塞和非阻塞：从cpu的消耗来讲，阻塞就是cpu停下来等待一个很慢的操作完成后，cpu才会完成其他的操作。

Java中的适配器模式和装饰器模式。

### 问题
```
数据读写一旦有阻塞，线程将会失去cpu的使用权，这在大规模访问量和有性能要求的情况下是不能被接受的。

如果可分配的端口号偏少，在遇到大量并发请求是就会成为瓶颈。由于端口有限导致大量请求等待连接。


```
