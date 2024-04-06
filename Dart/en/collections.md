# Dart Collections

Dart collections are a group or list of items. The Dart language provides built-in support for the following types of collections:

1. **List**: A List is an ordered group of items. The List data type in Dart is synonymous to arrays in other languages.

    ```
    List<int> numbers = [1, 2, 3, 4, 5];
    ```

2. **Set**: A Set is an unordered group of unique items. It is different from List as it contains unique elements.

    ```
    Set<String> colors = {'red', 'green', 'blue'};
    ```

3. **Queue**: Queue is a collection of items that are inserted at the end (also known as enqueue) and removed from the beginning (also known as dequeue).

    ```
    Queue items = new Queue();
    items.add(10);
    items.add(20);
    ```

4. **Map**: A Map is an unordered collection of key-value pairs, similar to a dictionary in Python or an object in JavaScript.

    ```
    Map<String, int> fruits = {
      'apples': 5,
      'bananas': 10,
      'oranges': 8
    };
    ```

Each of these collections has its own properties and methods which can be used based on the requirement.
