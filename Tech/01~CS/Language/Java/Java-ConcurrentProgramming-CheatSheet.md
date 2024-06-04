# Java Concurrent Programming CheatSheet

当出现线程活跃性问题时，我们可以借助一些工具进行诊断:

- Jstack。通过 jstack 命令，获取线程执行信息，找出其中的线程阻塞和死锁问题。

- Heap dump。通过 jmap 命令 dump 出当前的 jvm 堆栈信息，然后使用内存分析工具识别线程阻塞和死锁。

- Arthas。作为阿里开源的 Java 诊断利器，arthas 也提供了线程分析诊断功能, 可以通过 arthas 的 thread 命令，查找出当前阻塞的线程。

java.util.concurrent 包提供了一系列的并发工具类，让我们能够站在巨人的肩膀上，更加高效地实现并发程序。需要注意的是，我们一定要在正确地理解了当前所要处理的并发问题，以及工具类的机制原理之后，再去选择相应的并发工具类。如果只是一知半解就去盲目使用，很可能会给自己挖坑。

# Concurrent Primitive | 并发单元

常见的 Runnable、Callable、Future、FutureTask 这几个与线程相关的类或者接口：

- Runnable 应该是我们最熟悉的接口，它只有一个 run()函数，用于将耗时操作写在其中，该函数没有返回值。然后使用某个线程去执行该 runnable 即可实现多线程，Thread 类在调用 start()函数后就是执行的是 Runnable 的 run()函数。

- Callable 与 Runnable 的功能大致相似，Callable 中有一个 call()函数，但是 call()函数有返回值，而 Runnable 的 run()函数不能将结果返回给客户程序。

- Executor 就是 Runnable 和 Callable 的调度容器，Future 就是对于具体的 Runnable 或者 Callable 任务的执行结果进行取消、查询是否完成、获取结果、设置结果操作。get 方法会阻塞，直到任务返回结果。

- FutureTask 则是一个 RunnableFuture<V>，而 RunnableFuture 实现了 Runnbale 又实现了 Futrue<V> 这两个接口。

## Threads & Runnables

# Thread Pool | 线程池

## Executors

在并发程序中，线程的创建和管理是一个重要的命题。实际的生产代码中，不能为每一个任务就创建一个线程，也就是不能出现 new Thread(runnable).start()这样的代码，因为线程是昂贵的系统资源，不能无节制地创建，需要使用线程池对线程进行管理。Excutor 类支持了线程资源的管理和多线程任务的调度。可以使用 Executors 中的静态方法之一来创建一种线程池(newFixedThreadPool、newCachedThreadPool、newSingleThreadPool、newScheduledThreadPool 等)，可以使用 Runalbe、Callable 来提交并发任务，Excutor 类会自己负责任务的调度，解耦了任务的提交和执行。

```java
Callable<Integer> task = () -> {
    try {
        TimeUnit.SECONDS.sleep(1);
        return 123;
    }
    catch (InterruptedException e) {
        throw new IllegalStateException("task interrupted", e);
    }
};

ExecutorService executor = Executors.newFixedThreadPool(1);
Future<Integer> future = executor.submit(task);

System.out.println("future done? " + future.isDone());

Integer result = future.get();

System.out.println("future done? " + future.isDone());
System.out.print("result: " + result);
```

在使用 Excutor 时，如果线程池的任务之间存在依赖，线程池中的某些任务需要无限期地等待一些其它任务提供的资源；或者某些任务运行耗时较长，其它任务得不到运行资源，则会出现线程饥饿，引发活跃性问题，需要避免。

## Fork/Join

# 线程协作

## Atomic Variables | 原子性与原子变量

从 Java5.0 开始，提供了一组原子类变量(例如 AtomicInteger,AtomicLong,AtomicBoolean,AtomicReference 等)，来支持对单个变量的原子性操作。内置的监视器锁，是一种悲观锁，任何时候只有一个线程可以持有该锁，其它想获取该锁的线程必须阻塞等待。而 Atomic 类提供了一种乐观机制，任何线程都可以尝试获取资源并更新，如果在更新的过程中存在来自其它线程的干扰，那么这个操作将失败并可以重试。

Atomic 的实现依赖于处理器提供的 CAS(Compare and Swap)指令。CAS 是一个原子性操作，包含三个操作数：需要读写的内存位置 V、旧值 A 和拟写入的新值 B。线程读取 V 的值，如果等于 A，则将 V 的值更新为 B，返回成功，否则返回失败。

```java
@ThreadSafe
public class SafeSequence {
  private AtomicInteger value;

  /**
   * Returns a unique value.
   */
  public int getNext() {
    return value.getAndIncrement();
  }
}
```

相对于内置的监视器锁，Atomic 更加地轻量和高效，不存在死锁和活跃性问题。其主要劣势在于，需要调用者来处理竞争问题，决定在 CAS 操作失败时是重试、回退还是放弃。

## volatile | 可见性保障

## CountDownLatch

CountDownLatch 可以用来保证某些活动直到其它活动都完成之后才继续执行。

```java
public class TestHarness {
    public long timeTasks(int nThreads, final Runnable task)
            throws InterruptedException {
        final CountDownLatch startGate = new CountDownLatch(1);
        final CountDownLatch endGate = new CountDownLatch(nThreads);

        for (int i = 0; i < nThreads; i++) {
            Thread t = new Thread() {
                public void run() {
                    try {
                        startGate.await();
                        try {
                            task.run();
                        } finally {
                            endGate.countDown();
                        }
                    } catch (InterruptedException ignored) {
                    }
                }
            };
            t.start();
        }

        long start = System.nanoTime();
        startGate.countDown();
        endGate.await();
        long end = System.nanoTime();
        return end - start;
    }
```

# 锁与互斥

## Semaphore

信号量 Semaphore，用来控制同时访问某个特定资源的操作数量。Semaphore 中管理着一组虚拟许可，如果没有许可，则 acquire 操作将阻塞直到有许可。可以把锁看做一种特殊的二元信号量。

```java
public class BoundedHashSet<T> {
  private final Set<T> set;
  private final Semaphore sem;

  public BoundedHashSet(int bound) {
    this.set = Collections.synchronizedSet(new HashSet<T>());
    sem = new Semaphore(bound);
  }

  public boolean add(T o) throws InterruptedException {
    sem.acquire();
    boolean wasAdded = false;
    try {
      wasAdded = set.add(o);
      return wasAdded;
    } finally {
      if (!wasAdded) sem.release();
    }
  }

  public boolean remove(Object o) {
    boolean wasRemoved = set.remove(o);
    if (wasRemoved) sem.release();
    return wasRemoved;
  }
}
```

## Lock

Lock 类提供了一种可轮询的、定时的以及可中断的锁获取操作，当内置锁无法满足使用场景的要求时，可以考虑使用显式的 Lock。举一个带有时间限制的 Lock 示例:

```java
public class TimedLocking {
  private Lock lock = new ReentrantLock();

  public boolean trySendOnSharedLine(
    String message,
    long timeout,
    TimeUnit unit
  )
    throws InterruptedException {
    long nanosToLock = unit.toNanos(timeout) - estimatedNanosToSend(message);
    if (!lock.tryLock(nanosToLock, NANOSECONDS)) return false;
    try {
      return sendOnSharedLine(message);
    } finally {
      lock.unlock();
    }
  }
}
```

# Async Programming | 异步编程

## Callable & Future

## CompletableFuture

## RxJava

# Built-in ThreadSafe DataStructure | 内置的线程安全模型

## ConcurrentHashMap

为了解决线程活跃性问题，提高并发执行效率，一种可行的方案是降低锁的粒度。ConcurrentHashMap 可以看作这种思路的优秀实践，内部使用了分段锁(Lock Striping)的方式来降低锁的粒度，使用一个包含 16 个锁的数组，每个锁保护所有哈希桶的 1/16，其中第 N 个哈希桶，由 N%16 个锁来维护。其原理如下图所示:

![image.png](https://assets.ng-tech.icu/item/20230430222859.png)
