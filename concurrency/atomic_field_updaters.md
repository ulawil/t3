# Atomic Field updaters
Alternative to Atomics where the updated field is of regular type (e.g. int) and updated atomically by another class (Updater)
  
Example with `AtomicIntegerFieldUpdater`:
```java
public class SynchronizedExample {
    public volatile int i = 0;
}

SynchronizedExample se = new SynchronizedExample();

AtomicIntegerFieldUpdater<SynchronizedExample> iu =
    AtomicIntegerFieldUpdater.newUpdater(SynchronizedExample.class, "i");
    // i must be:
    // - volatile
    // - non-static
    // - not final

iu.incrementAndGet(se);
```
`i` must be:
- volatile - for CAS to work
- not final - needs to be able to be changed
- non-static - designed for updating fields of instances
