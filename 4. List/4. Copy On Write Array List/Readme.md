
---

# Thread-Safety in Java Lists & CopyOnWriteArrayList

---

## 1. Thread Safety of Java List Implementations

### ❌ ArrayList & LinkedList

* **Not thread-safe**
* Concurrent access (read + write) by multiple threads can cause:

  * Data inconsistency
  * `ConcurrentModificationException`
* Iterators are **fail-fast**

---

## 2. ConcurrentModificationException (CME)

### What is it?

* Thrown when a collection is **structurally modified** while being iterated
* Common with:

  * `ArrayList`
  * `LinkedList`
  * `HashMap`

---

## 3. Thread-Safe List Options

| Option                           | Thread-Safe | Locking Strategy    | Notes                                   |
| -------------------------------- | ----------- | ------------------- | --------------------------------------- |
| `Vector`                         | ✅           | Locks entire list   | Legacy, slow                            |
| `Collections.synchronizedList()` | ✅           | Locks entire list   | Manual synchronization during iteration |
| `CopyOnWriteArrayList`           | ✅           | Lock only on writes | Best for read-heavy workloads           |

---

## 4. Problem Demonstration: ArrayList with Multiple Threads

### ❌ Code: ArrayList with Concurrent Read & Write

```java
import java.util.*;

public class Main
{
    public static void main(String[] args) throws InterruptedException
    {
        List<Integer> list = new ArrayList<>();

        // Initial data
        for (int i = 1; i <= 5; i++)
        {
            list.add(i);
        }

        // Reader thread (ITERATION)
        Thread reader = new Thread(() ->
        {
            System.out.println("Reader started...");
            for (Integer value : list)
            {
                System.out.println("Reader reads: " + value);
                sleep(500);
            }
            System.out.println("Reader finished.");
        });

        // Writer thread (MODIFICATION)
        Thread writer = new Thread(() ->
        {
            sleep(800);
            System.out.println("\nWriter modifying list...");
            list.add(6);
            list.add(7);
            System.out.println("Writer added elements: 6, 7\n");
        });

        reader.start();
        writer.start();

        reader.join();
        writer.join();

        System.out.println("Final list contents: " + list);
    }

    private static void sleep(long millis)
    {
        try
        {
            Thread.sleep(millis);
        }
        catch (InterruptedException ignored) {}
    }
}
```

### ❌ Output

```
Reader started...
Reader reads: 1
Reader reads: 2

Writer modifying list...
Writer added elements: 6, 7

Exception in thread "Thread-0" java.util.ConcurrentModificationException
	at java.base/java.util.ArrayList$Itr.checkForComodification(ArrayList.java:1096)
	at java.base/java.util.ArrayList$Itr.next(ArrayList.java:1050)
	at Main.lambda$main$0(Main.java:22)
	at java.base/java.lang.Thread.run(Thread.java:1575)

Final list contents: [1, 2, 3, 4, 5, 6, 7]
```

### ❗ Key Insight

* Iterator detects structural modification
* Fails immediately (fail-fast)

---

## 5. CopyOnWriteArrayList — Read vs Write Behavior

### Key Characteristics

* ✅ Thread-safe
* 🔓 **Reads are lock-free**
* 🔒 **Writes acquire lock**
* Iterators work on **snapshot**

---

## 6. Code: CopyOnWriteArrayList Read vs Write Demo

```java
import java.util.List;
import java.util.concurrent.CopyOnWriteArrayList;

public class CopyOnWriteReadWriteDemo {

    public static void main(String[] args) throws InterruptedException {

        List<Integer> list = new CopyOnWriteArrayList<>();

        // Initial data
        for (int i = 1; i <= 5; i++) {
            list.add(i);
        }

        // ================= READ THREAD =================
        Thread reader = new Thread(() -> {
            log("Reader started iteration");
            for (Integer value : list) {
                log("Reader reads: " + value);
                sleep(400);
            }
            log("Reader finished iteration");
        }, "READER");

        // ================= WRITER 1 =================
        Thread writer1 = new Thread(() -> {
            log("Writer-1 trying to add 6");
            list.add(6);
            log("Writer-1 finished adding 6");
        }, "WRITER-1");

        // ================= WRITER 2 =================
        Thread writer2 = new Thread(() -> {
            log("Writer-2 trying to add 7");
            list.add(7);
            log("Writer-2 finished adding 7");
        }, "WRITER-2");

        reader.start();
        sleep(500);

        writer1.start();
        writer2.start();

        reader.join();
        writer1.join();
        writer2.join();

        log("Final list contents: " + list);
    }

    private static void sleep(long millis) {
        try {
            Thread.sleep(millis);
        } catch (InterruptedException ignored) {}
    }

    private static void log(String msg) {
        System.out.printf("[%d] [%s] %s%n",
                System.currentTimeMillis() % 100000,
                Thread.currentThread().getName(),
                msg);
    }
}
```

### ✅ Output

```
[12345] [READER] Reader started iteration
[12745] [READER] Reader reads: 1

[13001] [WRITER-1] Writer-1 trying to add 6
[13002] [WRITER-1] Writer-1 finished adding 6

[13003] [WRITER-2] Writer-2 trying to add 7
[13004] [WRITER-2] Writer-2 finished adding 7

[13145] [READER] Reader reads: 2
[13545] [READER] Reader reads: 3
[13945] [READER] Reader reads: 4
[14345] [READER] Reader reads: 5
[14745] [READER] Reader finished iteration

[14746] [main] Final list contents: [1, 2, 3, 4, 5, 6, 7]
```

### 🔑 Observation

* Reader **does not see 6 & 7**
* No exception
* Iterator works on snapshot

---

## 7. Internal Working of CopyOnWriteArrayList

### Core Mechanism

* Uses `ReentrantLock`
* Copies entire array on every write

### Pseudocode

```java
lock.lock();
try 
{
    Object[] newArray = Arrays.copyOf(oldArray, oldArray.length + 1);
    newArray[last] = element;
    array = newArray;
} 
finally 
{
    lock.unlock();
}
```

### How it Works

1. Acquire lock
2. Create new array
3. Copy old elements
4. Add new element
5. Update reference
6. Release lock

---

## 8. Follow-Up Interview Questions

### ❓ Why choose CopyOnWriteArrayList?

* Read-heavy workloads
* No locking during reads
* Safe iteration without synchronization
* No `ConcurrentModificationException`

---

### ❓ Performance Trade-Off

| Aspect | Impact                |
| ------ | --------------------- |
| Read   | Very fast (lock-free) |
| Write  | Slow (array copy)     |
| Memory | High overhead         |

---

### ❓ Best Use Cases

* Event listeners
* Observer pattern
* Configuration data
* GUI frameworks
* Caches with rare updates

---

### ❓ Downsides / Limitations

* Not suitable for frequent writes
* High memory consumption
* Readers may see stale data temporarily

---

### ❓ Iterator Concurrency

* Iterators use **snapshot**
* Immune to concurrent modifications
* Never throw `ConcurrentModificationException`

---

### ❓ Real-World Example

* GUI frameworks:

  * Rendering thread reads UI components
  * Background thread updates components
  * Safe rendering without locks

---

## 9. One-Line Summary (Interview Gold)

> **CopyOnWriteArrayList trades write performance and memory for extremely fast, lock-free, and safe concurrent reads using snapshot-based iteration.**

---

