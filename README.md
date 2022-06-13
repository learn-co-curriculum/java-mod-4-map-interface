# Map Interface

## Learning Goals

- Understand what kind of collections implement the `Map` interface.
- Explain the different methods provided by the `Map` interface.
- Create immutable maps.

## What is the Map Interface?

A `Map` collection implementation stores key-value pairs. The keys must always
be unique but the values can be the same for different keys.

The `Map` interface defines the methods to work with maps. The `K` represents
the type of key and `V` represents the type of associated values.

![Map interface diagram](https://curriculum-content.s3.amazonaws.com/java-mod-4/Map-Interface-Diagram.png)

## Map Interface Methods

There are several methods provided by the `Map` interface. Some of them are
similar to the methods defined in the `Collection` interface.

- `int size()` - returns the total elements in the map.
- `boolean isEmpty()` - returns `true` if the map doesn’t have any elements and
  `false` otherwise.
- `void clear()` - deletes all the elements in the map.
- `V put(K key, V value)` - assigns the `value` to the specified `key` in the
  map. It returns previously associated keys or `null` otherwise.
- `V putIfAbsent(K key, V value)` - assigns the provided `value` to the `key` if
  there’s no value associated with it yet. Returns `null` if a value was
  assigned or returns the previously stored value otherwise.
- `V get(Object key)` - returns the value assigned to the key or `null`
  otherwise.
- `V getOrDefault(Object key, V defaultValue)` - returns the value associated
  with the provided `key` or the `defaultValue` if the key didn’t have any value
  associated with it.
- `V remove(Object key)` - deletes the `key` from the map.
- `boolean containsKey(Object key)` - returns `true` if the key is in the map.
- `boolean containsValue(Object value)` - returns `true` if any of the keys
  contains the specified `value`
- `Set<K> keySet()` - returns the keys in the map as a `Set`.
- `Collection<V> values()` - returns all the values in the map as a
  `Collection`.
- `Set<Map.Entry<K, V>> entrySet()` - returns all the entries stored in the map
  as a `Set`.

These are the most common methods you’ll be using. You can check out more
methods [here](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html).

## Creating Immutable Maps

We can create immutable maps using the `of` method provided by the `Map`
interface. Let’s look at an example and check out what methods we can apply on
it.

```java
public class Example {
    public static void main(String[] args) {
        Map<String, String> userEmails = Map.of(
                "john", "john@example.com",
                "katy", "katy@example.com",
                "ammar", "ammar@example.com",
                "noam", "noam@example.com"
        );

        System.out.println(userEmails.size()); // 4
        System.out.println(userEmails.get("john")); // john@example.com
        System.out.println(userEmails.getOrDefault("alex", "unknown@example.com")); // unknown@example.com
        System.out.println(userEmails.containsKey("katy")); // true
        System.out.println(userEmails.containsValue("ammar@example.com")); // true

        userEmails.put("alex", "alex@example.com"); // error since the map is immutable
    }
}
```

## Iteration

We can use the `keySet`, `values`, and `entrySet` methods to iterate through
maps.

```java
public class Example {
    public static void main(String[] args) {
        Map<String, String> userEmails = Map.of(
                "john", "john@example.com",
                "katy", "katy@example.com",
                "ammar", "ammar@example.com",
                "noam", "noam@example.com"
        );

        // print all the usernames
        System.out.println("Usernames:");
        for (String name: userEmails.keySet()) {
            System.out.println(name);
        }

        // print all the user emails
        System.out.println("\n\nUser Emails:");
        for (String email: userEmails.values()) {
            System.out.println(email);
        }

        // print both usernames and the associated emails
        System.out.println("\n\nEntries:");
        for (Map.Entry<String, String> entry: userEmails.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}
```

Here’s the output for the above code:

```plaintext
Usernames:
ammar
john
katy
noam

User Emails:
ammar@example.com
john@example.com
katy@example.com
noam@example.com

Entries:
ammar: ammar@example.com
john: john@example.com
katy: katy@example.com
noam: noam@example.com
```

## References

- [Map Java docs](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html)
