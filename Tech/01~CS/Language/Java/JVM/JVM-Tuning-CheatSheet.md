# JVM 调试与优化实践清单

本文着重于介绍 JVM 线上问题定位中常用的调试命令与工具，对于具体的应用案例请参考其他章节。

# 调试工具

常见的调试工具会提供慢调用自动监听、全局线程比对、热点方法分析等功能。

# JVM 参数配置分析

## 基础参数

- `-Xms4g`: JVM 启动时，分配的最小堆大小 4G

## 垃圾回收参数

## 其他参数

## Tomcat JVM 配置

```sh
CATALINA_OPTS="-server"
CATALINA_OPTS="${CATALINA_OPTS} -Xms5120m -Xmx5120m"
CATALINA_OPTS="${CATALINA_OPTS} -XX:PermSize=256m -XX:MaxPermSize=256m"
CATALINA_OPTS="${CATALINA_OPTS} -Xmn2500m"
CATALINA_OPTS="${CATALINA_OPTS} -XX:MaxDirectMemorySize=1g"
CATALINA_OPTS="${CATALINA_OPTS} -XX:SurvivorRatio=10"
CATALINA_OPTS="${CATALINA_OPTS} -XX:+UseConcMarkSweepGC -XX:+UseCMSCompactAtFullCollection -XX:CMSMaxAbortablePrecleanTime=5000"
CATALINA_OPTS="${CATALINA_OPTS} -XX:+CMSClassUnloadingEnabled -XX:CMSInitiatingOccupancyFraction=80 -XX:+UseCMSInitiatingOccupancyOnly"
CATALINA_OPTS="${CATALINA_OPTS} -XX:+ExplicitGCInvokesConcurrent -Dsun.rmi.dgc.client.gcInterval=72000000"
CATALINA_OPTS="${CATALINA_OPTS} -XX:ParallelGCThreads=${CPU_COUNT}"
CATALINA_OPTS="${CATALINA_OPTS} -Xloggc:${MIDDLEWARE_LOGS}/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps"
CATALINA_OPTS="${CATALINA_OPTS} -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=${MIDDLEWARE_LOGS}/java.hprof"
CATALINA_OPTS="${CATALINA_OPTS} -Djava.awt.headless=true"
CATALINA_OPTS="${CATALINA_OPTS} -Dsun.net.client.defaultConnectTimeout=10000"
CATALINA_OPTS="${CATALINA_OPTS} -Dsun.net.client.defaultReadTimeout=30000"
CATALINA_OPTS="${CATALINA_OPTS} -DJM.LOG.PATH=${MIDDLEWARE_LOGS}"
CATALINA_OPTS="${CATALINA_OPTS} -Dfile.encoding=${JAVA_FILE_ENCODING}"
CATALINA_OPTS="${CATALINA_OPTS} -Djava.awt.headless=true -Dcom.sun.management.jmxremote.port=1090"
CATALINA_OPTS="${CATALINA_OPTS} -Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.ssl=false"
CATALINA_OPTS="${CATALINA_OPTS} -Dcom.sun.management.jmxremote.authenticate=false -Djava.rmi.server.hostname=10.125.59.163"
```

| 参数                                                        | 含义                                                                                                                                                                                                                                                                                                                                                                                      | 扩展阅读                                                                                                                                                      |
| ----------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| -Xms4g                                                      |                                                                                                                                                                                                                                                                                                                                                                                           |                                                                                                                                                               |
| -Xmx4g                                                      | jvm 启动时，允许分配的最大的堆大小：4g                                                                                                                                                                                                                                                                                                                                                    |                                                                                                                                                               |
| -XX:MetaspaceSize=256m                                      | 元数据区默认大小，从 JDK8 之后，没有 Perm 区了                                                                                                                                                                                                                                                                                                                                            |                                                                                                                                                               |
| -XX:MaxMetaspaceSize=256m                                   | 元数据的最大大小                                                                                                                                                                                                                                                                                                                                                                          |                                                                                                                                                               |
| -Xmn2g                                                      | 分配的年轻代大小：2g                                                                                                                                                                                                                                                                                                                                                                      |                                                                                                                                                               |
| -XX:MaxDirectMemorySize=1g                                  | 配置最大的堆外内存                                                                                                                                                                                                                                                                                                                                                                        | <http://hellojava.info/?tag=maxdirectmemorysize>                                                                                                              |
| -XX:SurvivorRatio=10                                        | Eden 区与 Survivor 区的大小比值                                                                                                                                                                                                                                                                                                                                                           |                                                                                                                                                               |
| -XX:+UseConcMarkSweepGC                                     | 使用 CMS 内存收集                                                                                                                                                                                                                                                                                                                                                                         |                                                                                                                                                               |
| -XX:+UseCMSCompactAtFullCollection                          | 在 FULL GC 的时候，对年老代的压缩                                                                                                                                                                                                                                                                                                                                                         | CMS 是不会移动内存的，因此，这个非常容易产生碎片，导致内存不够用，因此，内存的压缩这个时候就会被启用。增加这个参数是个好习惯。可能会影响性能,但是可以消除碎片 |
| -XX:CMSMaxAbortablePrecleanTime=5000                        | 指定 CMS-concurrent-abortable-preclean 阶段执行的时间，该阶段主要是执行一些预清理，减少应用暂停的时间。但在 JDK 5.0+、6.0+的版本中有可能会由于 JDK 的 bug29 导致 CMS 在 remark 完毕后很久才触发 sweeping 动作。通过设置-XX: CMSMaxAbortablePrecleanTime=5（单位为 ms）来避免，                                                                                                            | <http://shensy.iteye.com/blog/1915227> <http://www.blogjava.net/BlueDavy/archive/2009/10/09/297562.html>                                                      |
| -XX:+CMSClassUnloadingEnabled                               | 由于使用的框架是 Spring/Hibernate 大量采用 cglib，导致生成的 Proxy 会比较多，而这些是存放在 PermGen 区域，sun JDK 默认情况下不会去回收，必须加上-XX:+CMSClassUnloadingEnabled -XX:+CMSPermGenSweepingEnabled 参数，JDK 才会去回收这部分数据                                                                                                                                               |                                                                                                                                                               |
| -XX:CMSInitiatingOccupancyFraction=80                       | 使用 cms 作为垃圾回收使用 80％后开始 CMS 收集                                                                                                                                                                                                                                                                                                                                             |                                                                                                                                                               |
| -XX:+UseCMSInitiatingOccupancyOnly                          | 我们用-XX+UseCMSInitiatingOccupancyOnly 标志来命令 JVM 不基于运行时收集的数据来启动 CMS 垃圾收集周期。而是，当该标志被开启时，JVM 通过 CMSInitiatingOccupancyFraction 的值进行每一次 CMS 收集，而不仅仅是第一次。然而，请记住大多数情况下，JVM 比我们自己能作出更好的垃圾收集决策。因此，只有当我们充足的理由(比如测试)并且对应用程序产生的对象的生命周期有深刻的认知时，才应该使用该标志 |                                                                                                                                                               |
| -XX:+ExplicitGCInvokesConcurrent                            | 如今,被广泛接受的最佳实践是避免显式地调用 GC(所谓的“系统 GC”)，即在应用程序中调用 system.gc()。然而，这个建议是不管使用的 GC 算法的，值得一提的是，当使用 CMS 收集器时，系统 GC 将是一件很不幸的事，因为它默认会触发一次 Full GC。幸运的是，有一种方式可以改变默认设置。标志-XX:+ExplicitGCInvokesConcurrent 命令 JVM 无论什么时候调用系统 GC，都执行 CMS GC，而不是 Full GC，            | -                                                                                                                                                             |
| -Dsun.rmi.dgc.server.gcInterval=2592000000                  | 作为 rmi-server 时，gc 的时间间隔，默认是 1 小时，720 小时                                                                                                                                                                                                                                                                                                                                | <https://coderanch.com/t/91073/Difference-client-gcInterval-server-gcInterval>                                                                                |
| -Dsun.rmi.dgc.client.gcInterval=2592000000                  | 作为 rmi-client 时，gc 的时间间隔，默认是 1 小时，720 小时                                                                                                                                                                                                                                                                                                                                | <https://coderanch.com/t/91073/Difference-client-gcInterval-server-gcInterval>                                                                                |
| -XX:ParallelGCThreads=4                                     | 并行收集器的线程数                                                                                                                                                                                                                                                                                                                                                                        | 此值最好配置与处理器数目相等 同样适用于 CMS                                                                                                                   |
| -Xloggc:/home/admin/logs/gc.log                             | gc 打印的日志目录                                                                                                                                                                                                                                                                                                                                                                         | -                                                                                                                                                             |
| -XX:+PrintGCDetails                                         | 打印 GC 的详情信息                                                                                                                                                                                                                                                                                                                                                                        | -                                                                                                                                                             |
| -XX:+PrintGCDateStamps                                      | 打印 GC 的时间戳                                                                                                                                                                                                                                                                                                                                                                          | -                                                                                                                                                             |
| -XX:+HeapDumpOnOutOfMemoryError                             | 当发生 OOM 错误 时，将内存 DUMP 下来                                                                                                                                                                                                                                                                                                                                                      | -                                                                                                                                                             |
| -XX:HeapDumpPath=/home/admin/logs/java.hprof                | 内存 DUMP 的路径                                                                                                                                                                                                                                                                                                                                                                          | -                                                                                                                                                             |
| -Djava.awt.headless=true                                    | Headless 模式是在缺少显示屏、键盘或者鼠标时的系统配置                                                                                                                                                                                                                                                                                                                                     | -                                                                                                                                                             |
| -Dsun.net.client.defaultConnectTimeout=10000                | java.net.URLConnection 默认的连接超时时间，毫秒数单位                                                                                                                                                                                                                                                                                                                                     | -                                                                                                                                                             |
| -Dsun.net.client.defaultReadTimeout=30000                   | 设置超时时间，当从 inputstream 进行读取的时候                                                                                                                                                                                                                                                                                                                                             | -                                                                                                                                                             |
| -DJM.LOG.PATH=/home/admin/logs                              | 阿里中间件约定定义日志文件路径                                                                                                                                                                                                                                                                                                                                                            | -                                                                                                                                                             |
| -DJM.SNAPSHOT.PATH=/home/admin/snapshots                    | 容灾文件，原来和日志一个目录，现在单独指定，防止运维误删, 如 diamond，configclient                                                                                                                                                                                                                                                                                                        | -                                                                                                                                                             |
| -Dfile.encoding=UTF-8                                       | 设置文件编码为 UTF-8，Charset.defaultCharset()                                                                                                                                                                                                                                                                                                                                            | -                                                                                                                                                             |
| -Dhsf.publish.delayed=true                                  | true 意思是启动延迟发布,也就是不向 configserver 上注册地址,等待用户通过 online hsf 触发将 hsf 服务地址,注册到 configserver 去,才能提供使用(这种场景下 -Dhsf.publish.delayed=true 和 online hsf 必须同时使用,缺一不可);                                                                                                                                                                    |                                                                                                                                                               |
| -Dproject.name=di-afi                                       | 设置工程名，与应用名相同                                                                                                                                                                                                                                                                                                                                                                  | -                                                                                                                                                             |
| -Dpandora.boot.wait=true                                    | PandoraBootstrap.markAndWait()，标记这里是不是要等待的，                                                                                                                                                                                                                                                                                                                                  | -                                                                                                                                                             |
| -Dlog4j.defaultInitOverride=true                            | 检查系统属性 log4j.defaultInitOverride，如果该属性被设置为 false，则执行初始化；否则（只要不是 false，无论是什么值，甚至没有值，都是否则），跳过初始化，                                                                                                                                                                                                                                  | -                                                                                                                                                             |
| -Dpandora.location=/home/admin/di-afi/target/taobao-hsf.sar | 设置潘多拉的路径                                                                                                                                                                                                                                                                                                                                                                          | -                                                                                                                                                             |
| -Dapp.location=/home/admin/di-afi/target/di-afi             | 设置应用的路径                                                                                                                                                                                                                                                                                                                                                                            | -                                                                                                                                                             |
| -Djava.endorsed.dirs                                        | 包升级替换机制，一般默认是 lib/endorsed 文件夹，就是说，可以把你自己的 jar 包放在这里，代替原有的系统的 jar 包                                                                                                                                                                                                                                                                            | -                                                                                                                                                             |
| -Djava.io.tmpdir=/home/admin/di-afi/.default/temp           | 设置应用的写入的临时文件目录                                                                                                                                                                                                                                                                                                                                                              | -                                                                                                                                                             |

# 内存分析

Full GC 每小时小于个位数

# 线程与调用分析

# 追踪

# JVM 常用调试命令与工具介绍

本文着重于介绍 JVM 线上问题定位中常用的调试命令与工具，对于具体的应用案例请参考其他章节。

# 内存

Full GC 每小时小于个位数

## Dump

JEP 328: Flight Recorder（JFR）是 Oracle 刚刚开源的强大特性。而 JFR 是一套集成进入 JDK、JVM 内部的事件机制框架，通过良好架构和设计的框架，硬件层面的极致优化，生产环境的广泛验证，它可以做到极致的可靠和低开销。在 SPECjbb2015 等基准测试中，JFR 的性能开销最大不超过 1%。

```sh
# Time-Based
$ java -XX:StartFlightRecording=delay=20s,duration=60s,filename=C:\myRecording.jfr,settings=profile,name=SampleRecording

# Continuous With Dump on Demand
$ java -XX:StartFlightRecording=settings=default

# Continuous With Dump on Exit
$ java -XX:StartFlightRecording=settings=default -XX:FlightRecorderOptions=dumponexit=true,dumponexitpath=C:\tmp
```

通过 jmap 命令生成 dump 文件
命令格式：jmap -dump:live,format=b,file=heap.bin <pid>
注意：如果要保留 heapdump 中的不可达对象，则需要把”:live“去掉，即使用命令”jmap -dump,format=b,file=heap.bin <pid>“
通过设置 JVM 参数自动生成 使用-XX:+HeapDumpOnOutOfMemoryError 这个 JVM 参数，在 Java 进程运行过程中发生 OOM 的时候就会生成一个 heapdump 文件，并写入到指定目录，一般用-XX:HeapDumpPath=\${HOME}/logs/test 来设置。

# 线程

# 网络

# 磁盘

# 追踪

# Links

- [JVM 监控与调优](http://my.oschina.net/91jason/blog/493870?p={{page}})

[诊断 Java 代码中常见的数据库性能热点问题](http://www.infoq.com/cn/articles/Diagnosing-Common-Java-Database-Performance-Hotspots) [大神手把手教你 Java 性能优化 - 江南白衣(加强版)](http://mp.weixin.qq.com/s?__biz=MzI3MzEzMDI1OQ==&mid=2651815337&idx=1&sn=8e846e11e908735a5175c9eacb642329)

- [关键业务系统的 JVM 启动参数推荐](http://calvin1978.blogcn.com/articles/jvmoption-2.html) [关键业务系统的 JVM 参数推荐 (2016 热冬版 )](http://calvin1978.blogcn.com/articles/jvmoption-2.html?f=tt)

- [JVM 调试工具说明](http://blog.csdn.net/jiushuai/article/details/8455788) >[Java VisualVM ](http://ihuangweiwei.iteye.com/blog/1219302) >[JMX](http://docs.oracle.com/javase/tutorial/jmx/):Java Management Extensions (JMX)
