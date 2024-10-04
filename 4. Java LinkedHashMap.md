### Java LinkedHashMap

Java LinkedHashMap is a hash table and doubly linked List based implementation of Java’s Map interface. 
It extends the HashMap class which is another very commonly used implementation of the Map interface.

![image](https://github.com/user-attachments/assets/ce2aa3ca-915a-402b-a433-756cc9900889)

The HashMap class doesn’t guarantee any specific iteration order of the elements. It doesn’t keep track of the order in which the elements are inserted, and produces the elements in a random order every time you iterate over it.

If you want a predictable iteration order of the elements in a Map, then you can use a LinkedHashMap.

The iteration order in a LinkedHashMap is normally the order in which the elements are inserted. However, it also provides a special constructor using which you can change the iteration order from the least-recently accessed element to the most-recently accessed element and vice versa. This kind of iteration order can be useful in building LRU caches. In any case, the iteration order is predictable.

**Following are some important points to note about LinkedHashMap in Java -**
1. A LinkedHashMap cannot contain duplicate keys.
2. LinkedHashMap can have null values and the null key.
3. Unlike HashMap, the iteration order of the elements in a LinkedHashMap is predictable.
4. Just like HashMap, LinkedHashMap is not thread-safe. You must explicitly synchronize concurrent access to a LinkedHashMap in a multi-threaded environment.

### Creating and Initializing a LinkedHashMap

**The following example shows how to create a LinkedHashMap and add new key-value pairs to it.**

```
import java.util.LinkedHashMap;

public class CreateLinkedHashMapExample {
    public static void main(String[] args) {
        // Creating a LinkedHashMap
        LinkedHashMap<String, Integer> wordNumberMapping = new LinkedHashMap<>();

        // Adding new key-value pairs to the LinkedHashMap
        wordNumberMapping.put("one", 1);
        wordNumberMapping.put("two", 2);
        wordNumberMapping.put("three", 3);
        wordNumberMapping.put("four", 4);

        // Add a new key-value pair only if the key does not exist in the LinkedHashMap, or is mapped to `null`
        wordNumberMapping.putIfAbsent("five", 5);

        System.out.println(wordNumberMapping);
    }
}
```

### Accessing the entries of a LinkedHashMap

**This example shows how to**
1. Check if a key exists in a LinkedHashMap.
2. Check if a value exists in the LinkedHashMap.
3. Modify the value associated with a given key in the LinkedHashMap.

```
import java.util.LinkedHashMap;

public class AccessEntriesFromLinkedHashMapExample {
    public static void main(String[] args) {
        LinkedHashMap<Integer, String> customerIdNameMapping = new LinkedHashMap<>();

        customerIdNameMapping.put(1001, "Jack");
        customerIdNameMapping.put(1002, "David");
        customerIdNameMapping.put(1003, "Steve");
        customerIdNameMapping.put(1004, "Alice");
        customerIdNameMapping.put(1005, "Marie");

        System.out.println("customerIdNameMapping : " + customerIdNameMapping);

        // Check if a key exists in the LinkedHashMap
        Integer id = 1005;
        if(customerIdNameMapping.containsKey(id)) {
            System.out.println("Found the customer with id " + id + " : " + customerIdNameMapping.get(id));
        } else {
            System.out.println("Customer with id " + id + " does not exist");
        }

        // Check if a value exists in the LinkedHashMap
        String name = "David";
        if(customerIdNameMapping.containsValue(name)) {
            System.out.println("A customer named " + name + " exist in the map");
        } else {
            System.out.println("No customer found with name " + name + " in the map");
        }

        // Change the value associated with an existing key
        id = 1004;
        customerIdNameMapping.put(id, "Bob");
        System.out.println("Changed the name of customer with id " + id + ", New mapping : " + customerIdNameMapping);
    }
}
```


### Removing entries from a LinkedHashMap

**The example below shows how to**

1. Remove a key from a LinkedHashMap.
2. Remove a key from a LinkedHashMap only if it is associated with the given value.

```
import java.util.LinkedHashMap;

public class RemoveEntriesFromLinkedHashMapExample {
    public static void main(String[] args) {
        LinkedHashMap<String, String> husbandWifeMapping = new LinkedHashMap<>();

        husbandWifeMapping.put("Rajeev", "Jennifer");
        husbandWifeMapping.put("John", "Maria");
        husbandWifeMapping.put("Chris", "Lisa");
        husbandWifeMapping.put("Steve", "Susan");

        System.out.println("husbandWifeMapping : " + husbandWifeMapping);

        // Remove a key from the LinkedHashMap
        String wife = husbandWifeMapping.remove("John");
        System.out.println("Removed John and his wife " + wife + " from the mapping. New husbandWifeMapping : " + husbandWifeMapping);

        // Remove a key from the LinkedHashMap only if it is mapped to the given value
        boolean isRemoved = husbandWifeMapping.remove("John", "Susan");
        System.out.println("Did John get removed from the mapping? : " + isRemoved);
    }
}
```


### Iterating over a LinkedHashMap

**The example in this section shows various ways of iterating over a LinkedHashMap:**

1. Iterate over a LinkedHashMap using Java 8 forEach and lambda expression.
2. Iterate over a LinkedHashMap’s entrySet using Java 8 forEach and lambda expression.
3. Iterate over a LinkedHashMap’s entrySet using iterator().
4. Iterate over a LinkedHashMap’s entrySet using iterator() and Java 8 forEachRemaining() method.

```
import java.util.Iterator;
import java.util.LinkedHashMap;
import java.util.Map;

public class IterateOverLinkedHashMapExample {
    public static void main(String[] args) {
        LinkedHashMap<String, String> userCityMapping = new LinkedHashMap<>();

        userCityMapping.put("Rajeev", "Bengaluru");
        userCityMapping.put("Chris", "London");
        userCityMapping.put("David", "Paris");
        userCityMapping.put("Jesse", "California");

        System.out.println("=== Iterating over a LinkedHashMap using Java 8 forEach and lambda ===");
        userCityMapping.forEach((user, city) -> {
            System.out.println(user + " => " + city);
        });

        System.out.println("\n=== Iterating over the LinkedHashMap's entrySet using Java 8 forEach and lambda ===");
        userCityMapping.entrySet().forEach(entry -> {
            System.out.println(entry.getKey() + " => " + entry.getValue());
        });

        System.out.println("\n=== Iterating over the entrySet of a LinkedHashMap using iterator() ===");
        Iterator<Map.Entry<String, String>> userCityMappingIterator = userCityMapping.entrySet().iterator();
        while (userCityMappingIterator.hasNext()) {
            Map.Entry<String, String> entry = userCityMappingIterator.next();
            System.out.println(entry.getKey() + " => " + entry.getValue());
        }

        System.out.println("\n=== Iterating over the entrySet of a LinkedHashMap using iterator() and forEachRemaining ===");
        userCityMappingIterator = userCityMapping.entrySet().iterator();
        userCityMappingIterator.forEachRemaining(entry -> {
            System.out.println(entry.getKey() + " => " + entry.getValue());
        });
    }
}
```
