Knows synchronization principles and primitives. Is able to write thread-safe code in the language of choice.
Knows basics of cross-thread communication.
Is aware of potential concurrency issues (deadlock, starvation).

* novice
    * synchronized
    * volatile
    * atomics
    * thread and thread pools
    * deadlock
* competent
    * await/notify
    * ForkJoinPool
    * Locks
    * ExecutorService
    * BlockingQueue
    * Atomic Field updaters
    * LongAdder, DoubleAdder
    * deadlock resolution

# Wait/notify
```java
    // used for thread coordination around a shared resource’s state

    wait(); // releases the monitor of the object this thread is synchronized on
            // and causes the current thread to enter the waiting state
            // until it is awakened by notify(), notifyAll(), or interrupted

    notify(); // wakes up one random thread waiting on this object's monitor

    notifyAll(); // wakes up all threads waiting on this object's monitor
```

# Locks
```java
    public static Lock lock = new ReentrantLock(true); // fairness set to true
    // offers similar semantics and concurrency as implicit lock of synchronized method, but with extended capabilities:
    // - does not need to be contained in 1 method
    // - supports fairness (longest waiting thread acquires the lock first)
    // - thread doesn't have to be blocked if it can't acquire a lock when using tryLock()
    // - waiting thread can be interrupted when using lockInterruptibly()

    public static ReadWriteLock readWriteLock= new ReentrantReadWriteLock();
    public static Lock readLock = readWriteLock.readLock();
    // if no thread acquired or tries to acquire write lock, multiple threads can acquire read lock
    public static Lock writeLock = readWriteLock.writeLock();
    // if no threads acquired read or write lock, only one thread can acquire write lock

    // working with locks:
    lock.lock();
    try {
        ...
    } finally {
        lock.unlock();
    }
```

# ExecutorService
```java
   // ExecutorService - tool that simplifies running tasks asynchronously by providing factory methods
   //                   for thread pools we can submit tasks to
        
   // Single thread executor example
   ExecutorService executorService1 = Executors.newSingleThreadExecutor();
   executorService1.submit(() -> System.out.println("Hello world"));
   executorService1.shutdown();

   // Thread pool example
   ExecutorService executorService2 = Executors.newFixedThreadPool(2);
   executorService2.submit(() -> System.out.println(Thread.currentThread().getName() + " - hello1!"));
   executorService2.submit(() -> System.out.println(Thread.currentThread().getName() + " - hello2!"));
   executorService2.submit(() -> System.out.println(Thread.currentThread().getName() + " - hello3!"));
   executorService2.shutdown();
   //          pool-2-thread-1 - hello1!
   //          pool-2-thread-2 - hello2!
   //          pool-2-thread-1 - hello3!

   // Scheduled executor example
   ScheduledExecutorService executorService3 = Executors.newSingleThreadScheduledExecutor();
   executorService3.schedule(() -> System.out.println("Hello world scheduled"), 5, TimeUnit.SECONDS);

   executorService3.scheduleAtFixedRate(() -> System.out.println("Hello world repeated"), 0, 5, TimeUnit.SECONDS);
   executorService3.awaitTermination(30, TimeUnit.SECONDS);
```






