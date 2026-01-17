
---

## What is HashMap?

`HashMap` is a **part of Java Collections Framework** that stores data in **key–value pairs**.

```text
Key → Value
```

Example:

```text
"name" → "Anubhav"
"role" → "SDE"
```

### Key points

* Stores **unique keys**
* Values **can be duplicated**
* **Order is NOT guaranteed**
* Allows **one null key** and **multiple null values**
* **Not thread-safe**

---

### 🔹 Core HashMap Methods Summary

| Method                                  | Purpose           | What it Does                                                                        | Return Value             |
| --------------------------------------- | ----------------- | ----------------------------------------------------------------------------------- | ------------------------ |
| `V get(K key)`                          | Fetch value       | Returns value for the key. If key doesn’t exist → **no exception**, returns `null`. | Value or `null`          |
| `V getOrDefault(K key, V defaultValue)` | Safe fetch        | If key absent **or mapped to null**, returns default value.                         | Value or default         |
| `V put(K key, V value)`                 | Insert / Update   | Adds new entry or updates existing key.                                             | Old value or `null`      |
| `V remove(Object key)`                  | Delete            | Removes key-value mapping if exists.                                                | Removed value or `null`  |
| `boolean containsKey(Object key)`       | Key check         | Checks if key exists in map.                                                        | `true / false`           |
| `boolean containsValue(Object value)`   | Value check       | Linear search for value in map.                                                     | `true / false`           |
| `V putIfAbsent(K key, V value)`         | Insert if missing | Inserts only if key absent or mapped to `null`.                                     | Existing value or `null` |
| `V compute(K key, BiFunction)`          | Atomic recompute  | Computes new value using key & old value. Returning `null` removes key.             | New value or `null`      |
| `V computeIfAbsent(K key, Function)`    | Lazy init         | Computes value only if key absent or null.                                          | Existing / new value     |
| `V computeIfPresent(K key, BiFunction)` | Update if present | Updates only if key exists and non-null.                                            | Updated value            |
| `V merge(K key, V value, BiFunction)`   | Combine values    | Inserts if absent, otherwise merges old & new.                                      | New value                |
| `Set<K> keySet()`                       | All keys          | Live view of keys. Changes affect map.                                              | `Set<K>`                 |
| `Collection<V> values()`                | All values        | Allows duplicates.                                                                  | `Collection<V>`          |
| `Set<Map.Entry<K,V>> entrySet()`        | Key-value pairs   | Best way to iterate map.                                                            | `Set<Entry>`             |

---

## 🧠 Complete Example Code

```java
import java.util.*;

public class Main
{
    public static void main(String[] args)
    {
        Map<String, Integer> map = new HashMap<>();

        map.put("Akash", 21);
        map.put("Yash", 16);
        map.put("Lav", 17);
        map.put("Rishika", 19);
        map.put("Harry", 18);

        System.out.println(map);

        System.out.println("Yash  = " + map.get("Yash"));
        System.out.println("Rahul = " + map.get("Rahul"));

        map.put("Akash", 25);
        System.out.println("Akash = " + map.get("Akash"));

        System.out.println("Akash = " + map.remove("Akash"));
        System.out.println("Rahul = " + map.remove("Rahul"));

        System.out.println(map);

        System.out.println("Lav = " + map.containsKey("Lav"));
        System.out.println("Doe = " + map.containsKey("Doe"));

        map.putIfAbsent("Rahul", 20);

        for (String key : map.keySet())
        {
            System.out.println(key + " = " + map.get(key));
        }

        for (int value : map.values())
        {
            System.out.print(value + " ");
        }
        System.out.println();

        for (Map.Entry<String, Integer> entry : map.entrySet())
        {
            System.out.println(entry.getKey() + " = " + entry.getValue());
        }

        System.out.println(map);

        System.out.println("Dev = " + map.getOrDefault("Dev", 56));
        System.out.println("Contains 18 = " + map.containsValue(18));

        // -------- compute() --------
        map.compute("Rahul", (k, v) -> v == null ? 10 : v + 1);
        map.compute("Dev", (k, v) -> v == null ? 10 : v + 1);

        // -------- computeIfAbsent() --------
        map.computeIfAbsent("Rahul", k -> 100);
        map.computeIfAbsent("Aman", k -> 15);

        // -------- computeIfPresent() --------
        map.computeIfPresent("Rahul", (k, v) -> v + 5);
        map.computeIfPresent("Suresh", (k, v) -> 50);

        // -------- merge() --------
        map.merge("Rahul", 2, Integer::sum);
        map.merge("Neha", 18, Integer::sum);

        System.out.println("Final Map: " + map);
    }
}
```

---

## 🧪 Sample Output (Order May Vary)

```
{Akash=21, Yash=16, Lav=17, Rishika=19, Harry=18}

Yash  = 16
Rahul = null
Akash = 25
Akash = 25
Rahul = null

{Yash=16, Lav=17, Rishika=19, Harry=18}

Lav = true
Doe = false

Yash = 16
Lav = 17
Rishika = 19
Harry = 18
Rahul = 20

16 17 19 18 20

Dev = 56
Contains 18 = true

Final Map:
{Yash=16, Lav=17, Rishika=19, Harry=18, Rahul=28, Dev=10, Aman=15, Neha=18}
```

---

## 🎯 Interview Gold Points

* `compute()` → **insert + update + delete** in one method
* Returning `null` in `compute / merge` → **key removed**
* `merge()` = best for **frequency counting**
* `entrySet()` = fastest iteration
* `HashMap` ≠ thread-safe
* Order not guaranteed (use `LinkedHashMap` if needed)

---
