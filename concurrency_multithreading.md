Knows synchronization principles and primitives. Is able to write thread-safe code in the language of choice.
Knows basics of cross-thread communication.
Is aware of potential concurrency issues (deadlock, starvation).

// novice
* synchronized, 
* volatile, 
* atomics, 
* thread and thread pools, 
* deadlock.
// competent
* await/notify, 
* ForkJoinPool, 
* Locks, 
* ExecutorService, 
* BlockingQueue, 
* Atomic Field updaters, 
* LongAdder, DoubleAdder, 
* deadlock resolution.

## Understanding internals of atomics
Internally, atomics make use of
- CAS (compare-and-swap) operation (not an algorithm but a single JVM instruction)
- volatile memory semantics (visibility + ordering)
to achieve thread-safe operations.

### CAS
`incrementAndGet()` CAS example:
```java
int prev, next;
do {
    prev = value; // 1
    next = prev + 1; // 2
} while (!CAS(value, prev, next)); // 3
return next;
```
1. read current value
2. calculate new value
3. compare if current value is the same (value == prev) and if yes, swap to new value (value = next); if not, retry the loop




