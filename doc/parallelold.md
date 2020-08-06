#### Parallel Old

```text

Parallel Old收集器和Serial Old收集器一样，工作在JAVA虚拟机的老年代。这种垃圾收集器使用多线程和“标记－整理”算法。它在JDK 1.6中才开始提供。

Parallel Old收集器是Parallel Scavenge收集器的老年代版本，用于老年代的垃圾回收，但与Parallel Scavenge不同的是，它使用的是“标记-整理算法”。适用于注重于吞吐量及CPU资源敏感的场合。

使用方式：-XX:+UseParallelOldGC，打开该收集器后，将使用Parallel Scavenge（年轻代）+Parallel Old（老年代）的组合进行GC。

在注重吞吐量及CPU资源敏感的场合，都可以优先考虑Parallel Scavenge加Parallel Old收集器。-XX:+ UseParallelOldGC对应parallel scavenge +parallel old 收集器。

Serial Old收集器是串行的进行垃圾回收，而Parallel old收集器是并行的进行垃圾回收。


```


### [GC介绍](../README.md)