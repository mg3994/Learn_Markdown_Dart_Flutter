# Dart Functions

In Dart, functions are objects and have a type, `Function`. This means functions can be assigned to variables or passed as arguments to other functions. You can also call an instance of a Dart class as if it were a function.

Here are the different types of functions in Dart:

1. **Top-level functions**: These are functions defined at the top level of the file, outside of any class.

    ```
    void main() {
      print('Hello, World!');
    }
    ```

2. **Static methods**: These are functions that are associated with a class but not with an instance of that class.

    ```
    class MyClass {
      static void myStaticFunction() {
        print('Hello, World!');
      }
    }
    ```

3. **Instance methods**: These are functions that are associated with an instance of a class.

    ```
    class MyClass {
      void myInstanceFunction() {
        print('Hello, World!');
      }
    }
    ```

4. **Anonymous functions**: These are unnamed functions that can be used as a parameter in a method call.

    ```
    var list = ['apples', 'bananas', 'oranges'];
    list.forEach((item) {
      print('${list.indexOf(item)}: $item');
    });
    ```

Each type of function has its own use case and can be used based on the requirement.
