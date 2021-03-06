#### Parallel Scavenge

##### What(是什么)

```text
Parallel Scavenge收集器是Java虚拟机中垃圾收集器的一种。
又称为吞吐量优先收集器，和ParNew收集器类似，是一个新生代收集器，同样是会停止用户线程。
使用复制算法的并行多线程收集器。Parallel Scavenge是Java1.8默认的收集器，
特点是并行的多线程回收，以吞吐量优先。
可以自适应调节收集策略

```


##### Why(为什么)


```text
Parallel Scavenge收集器的关注点与其他收集器不同， 
Parallel Scavenge收集器的目标则是达到一个可控制的吞吐量（Throughput）
(吞吐量=运行用户代码时间/(运行用户代码时间+垃圾收集时间))
如果虚拟机完成某个任务，用户代码加上垃圾收集总共耗费了100分钟，其中垃圾收集花掉1分钟，那吞吐量就是99%。

主要适合在后台运算而不需要太多交互的分析任务。

```
![as43uD.png](https://s1.ax1x.com/2020/08/05/as43uD.png)

##### How(怎么做)

```text

重要参数：
1、控制最大垃圾收集停顿时间的-XX:MaxGCPauseMillis参数
MaxGCPauseMillis参数允许的值是一个大于0的毫秒数，收集器将尽力保证内存回收花费的时间不超过设定值。
不过大家不要异想天开地认为如果把这个参数的值设置得稍小一点就能使得系统的垃圾收集速度变得更快，
GC停顿时间缩短是以牺牲吞吐量和新生代空间来换取的：系统把新生代调小一些，
收集300MB新生代肯定比收集500MB快吧，这也直接导致垃圾收集发生得更频繁一些，
原来10秒收集一次、每次停顿100毫秒，现在变成5秒收集一次、每次停顿70毫秒。停顿时间的确在下降，但吞吐量也降下来了。

2、直接设置吞吐量大小的 -XX:GCTimeRatio参数。
GCTimeRatio参数的值应当是一个大于0小于100的整数，也就是垃圾收集时间占总时间的比率。
如果把此参数设置为19，那允许的最大GC时间就占总时间的5%（即1 /（1+19）），
默认值为99，就是允许最大1%（即1 /（1+99））的垃圾收集时间。  


3、 UseAdaptiveSizePolicy开关参数。
-XX:+UseAdaptiveSizePolicy是一个开关参数，当这个参数打开之后，就不需要手工指定新生代的大小（-Xmn）
、Eden与Survivor区的比例（-XX:SurvivorRatio）、晋升老年代对象年龄（-XX:PretenureSizeThreshold）
等细节参数了，虚拟机会根据当前系统的运行情况收集性能监控信息，动态调整这些参数以提供最合适的停顿时间或最大
的吞吐量，这种调节方式称为GC自适应的调节策略（GC Ergonomics）。

使用方式：
-XX:+UseParallelGC强制使用该收集器，打开该收集器后，
将使用Parallel Scavenge（年轻代）+Serial Old(老年代)的组合进行GC。

-XX:+UseParallelOldGC，打开该收集器后，
将使用Parallel Scavenge（年轻代）+Parallel Old（老年代）的组合进行GC。
```

### [GC介绍](../README.md)