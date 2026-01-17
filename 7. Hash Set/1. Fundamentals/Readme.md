
---

## 🔹 What is `HashSet`?

`HashSet` is a **collection** in Java that:

* Stores **unique elements only**
* Does **NOT maintain insertion order**
* Is backed by a **hash table**
* Allows **one `null` value**

```java
HashSet<Integer> set = new HashSet<>();
```

---

## 🔹 HashSet Methods Explained

### 1️⃣ `add(value)`

Adds an element to the set

* Returns `true` if element was added
* Returns `false` if element already exists

```java
set.add(10);
```

---

### 2️⃣ `contains(value)`

Checks whether the value exists in the set

```java
set.contains(10); // true or false
```

---

### 3️⃣ `remove(value)`

Removes the specified element if present

```java
set.remove(20);
```

---

### 4️⃣ `clear()`

Removes **all elements** from the set

```java
set.clear();
```

---

### 5️⃣ `isEmpty()`

Checks if the set is empty

```java
set.isEmpty(); // true / false
```

---

## 🔹 Ways to Iterate Over HashSet

### ✅ 1. Enhanced for-loop

```java
for(int i : set) {
    System.out.println(i);
}
```

---

### ✅ 2. Iterator

```java
Iterator<Integer> itr = set.iterator();
while(itr.hasNext()) {
    System.out.println(itr.next());
}
```

---

### ✅ 3. forEach (Java 8)

```java
set.forEach(System.out::println);
```

---

## 🔹 Complete Java Program (Implementation)

```java
import java.util.HashSet;
import java.util.Iterator;

public class HashSetDemo {
    public static void main(String[] args) {

        HashSet<Integer> set = new HashSet<>();

        // add()
        set.add(10);
        set.add(20);
        set.add(30);
        set.add(10); // duplicate, ignored

        System.out.println("HashSet elements: " + set);

        // contains()
        System.out.println("Contains 20? " + set.contains(20));
        System.out.println("Contains 50? " + set.contains(50));

        // remove()
        set.remove(20);
        System.out.println("After removing 20: " + set);

        // isEmpty()
        System.out.println("Is set empty? " + set.isEmpty());

        // Iteration using for-each loop
        System.out.println("\nUsing enhanced for-loop:");
        for (int i : set) {
            System.out.println(i);
        }

        // Iteration using Iterator
        System.out.println("\nUsing Iterator:");
        Iterator<Integer> itr = set.iterator();
        while (itr.hasNext()) {
            System.out.println(itr.next());
        }

        // Iteration using forEach (Java 8)
        System.out.println("\nUsing forEach method:");
        set.forEach(System.out::println);

        // clear()
        set.clear();
        System.out.println("\nAfter clear(): " + set);
        System.out.println("Is set empty now? " + set.isEmpty());
    }
}
```

---

## 🔹 Sample Output (Order May Vary ⚠️)

```
HashSet elements: [10, 20, 30]
Contains 20? true
Contains 50? false
After removing 20: [10, 30]
Is set empty? false

Using enhanced for-loop:
10
30

Using Iterator:
10
30

Using forEach method:
10
30

After clear(): []
Is set empty now? true
```

---

## 🔹 Important Interview Points ⭐

* ❌ **No duplicates**
* ❌ **No guaranteed order**
* ✅ O(1) average time for `add`, `remove`, `contains`
* ✔ Best choice when **uniqueness is required**

---
