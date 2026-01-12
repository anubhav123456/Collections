# Java Collection Framework

---

## 1. What is Java Collection Framework (JCF)?

### What is a Collection?

* A **collection** is a **group of objects** (also called elements).
* Example: An array holding integers is also a collection.
* All collection-related classes and interfaces are present in **`java.util` package**.

### What is a Framework?

* A **framework** provides a **predefined architecture**.
* It consists of:

  * Interfaces
  * Classes
  * Methods
  * Ready-made functionality
* JCF provides built-in support for:

  * Add
  * Update
  * Delete
  * Search
  * Traverse elements

### Definition

> **Java Collection Framework** is a unified architecture that represents and manipulates a group of objects using predefined interfaces and classes.

### Java Version

* Introduced in **Java 1.2**

---

## 2. Why Do We Need Java Collection Framework?

### Before JCF (Pre-Java 1.2)

Available collections:

* Array
* Vector
* Hashtable

### Problem Before JCF

* No **common interface**
* Different syntax for:

  * Insertion
  * Retrieval
  * Removal
* Hard to remember APIs

### Example Without Common Interface

#### Array Example

```java
int[] arr = new int[4];
arr[0] = 1;
System.out.println(arr[0]);
```

#### Vector Example

```java
Vector<Integer> vector = new Vector<>();
vector.add(1);
System.out.println(vector.get(0));
```

➡ Different ways to **read/write** elements

### Solution by JCF

* Introduced **common interfaces**
* Same method names across collections
* Focus shifts from *how to use* → *which collection to use*

---

## 3. Java Collection Framework Hierarchy

### Two Major Categories

1. **Iterable → Collection** hierarchy
2. **Map** (separate hierarchy)

![JCF](pics/JCF1.jpg)
![JCF](pics/JCF2.jpg)

### Important Points

* **Map is NOT a child of Collection**
* Collection-based classes share common behavior

---

## 4. Iterable Interface

### Purpose

* Used to **traverse a collection**

### Java Version

* Added in **Java 1.5**

### Methods

* `iterator()` → Java 1.5
* `forEach()` → Java 1.8

---

## 5. Iteration Techniques



---

### 1️⃣ Using Iterator

```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class Main
{
    public static void main(String[] args)
    {
        List<Integer> values = new ArrayList<>();
        values.add(1);
        values.add(2);
        values.add(3);
        values.add(4);

        Iterator<Integer> iterator = values.iterator();

        while (iterator.hasNext())
        {
            int value = iterator.next();
            System.out.println(value);

            if(value == 3)
            {
                iterator.remove();
            }
        }

        System.out.println(values); // [1, 2, 4]

    }
}
```

#### Iterator Methods

* `hasNext()` → checks if elements remain
* `next()` → returns next element
* `remove()` → removes last returned element
---

### 2️⃣ Enhanced For Loop

```java
import java.util.ArrayList;
import java.util.List;

public class Main
{
    public static void main(String[] args)
    {
        List<Integer> values = new ArrayList<>();
        values.add(1);
        values.add(2);
        values.add(3);
        values.add(4);

        for(Integer value : values)
        {
            System.out.println(value);
        }

    }
}
```

✔ Works because Collection implements **Iterable**

---

### 3️⃣ forEach() Method (Java 1.8)

```java
import java.util.ArrayList;
import java.util.List;

public class Main
{
    public static void main(String[] args)
    {
        List<Integer> values = new ArrayList<>();
        values.add(1);
        values.add(2);
        values.add(3);
        values.add(4);

       //values.forEach(System.out::println); or
       values.forEach(val -> System.out.println(val));

    }
}
```

* Uses **lambda expression**
* Internally uses `Consumer<T>` functional interface

---

## 6. Collection Interface

### Purpose

* Represents a group of objects
* Defines common operations

### Java Version

* Added in **Java 1.2**

---

## 7. Commonly Used Collection Methods

### Method Summary

| Method        | Description                    | Java Version Introduced         |
| ------------- | ------------------------------ | ------------------------------- |
| size()        | Number of elements             | Java 1.2                        |
| isEmpty()     | Checks if empty                | Java 1.2                        |
| contains()    | Search element                 | Java 1.2                        |
| add()         | Insert element                 | Java 1.2                        |
| remove()      | Remove element                 | Java 1.2                        |
| addAll()      | Add another collection         | Java 1.2                        |
| removeAll()   | Remove common elements         | Java 1.2                        |
| containsAll() | Check full collection presence | Java 1.2                        |
| clear()       | Remove all elements            | Java 1.2                        |
| equals()      | Compare collections            | Java 1.2 *(Object override)*    |
| iterator()    | Iterate elements               | Java 1.2                        |
| stream()              | Creates a sequential stream to process collection elements one by one using functional operations.| Java 1.8 |
| parallelStream()      | Creates a parallel stream to process collection elements concurrently using multiple threads.     | Java 1.8 |

---

## 8. Collection Methods – Code Example

```java
List<Integer> values = new ArrayList<>();
values.add(2);
values.add(3);
values.add(4);
```

### size()

```java
System.out.println(values.size()); // 3
```

### isEmpty()

```java
System.out.println(values.isEmpty()); // false
```

### contains()

```java
System.out.println(values.contains(5)); // false
```

### add()

```java
values.add(5);
System.out.println(values.contains(5)); // true
```

### remove by index

```java
values.remove(3); // removes element at index 3 (value 5)
```

### remove by object

```java
values.remove(Integer.valueOf(3)); // removes value 3
```

---

## 9. addAll(), containsAll(), removeAll()

```java
Stack<Integer> stackValues = new Stack<>();
stackValues.add(6);
stackValues.add(7);
stackValues.add(8);
```

### addAll()

```java
values.addAll(stackValues);
```

### containsAll()

```java
System.out.println(values.containsAll(stackValues)); // true
```

### remove()

```java
values.remove(Integer.valueOf(7));
System.out.println(values.containsAll(stackValues)); // false
```

### removeAll()

```java
values.removeAll(stackValues);
```

### clear()

```java
values.clear();
System.out.println(values.isEmpty()); // true
```

---

## 10. Power of Collection Framework

* Same method names across all collections
* Easy to remember
* Focus on **use-case**, not syntax

Example:

```java
list.add();
stack.add();
queue.add();
```

---

## 11. Collection vs Collections

### Collection (No 's')

* Interface
* Part of JCF
* Represents a group of objects

### Collections (With 's')

* Utility class
* Contains only **static methods**
* Helps operate on collections

---

## 12. Collections Utility Methods

```java
List<Integer> list = new ArrayList<>();
list.add(1);
list.add(3);
list.add(2);
list.add(4);
```

### max()

```java
System.out.println(Collections.max(list)); // 4
```

### min()

```java
System.out.println(Collections.min(list)); // 1
```

### sort()

```java
Collections.sort(list);
System.out.println(list); // [1, 2, 3, 4]
```

---

