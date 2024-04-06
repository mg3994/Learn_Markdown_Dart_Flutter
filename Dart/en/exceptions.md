# Exception Handling in Dart

Exception handling is a process used in programming languages to handle the occurrence of errors that disrupt the normal flow of the program's instructions.

In Dart, we have the following ways to handle exceptions:

1. **try-catch**: We use the `try-catch` block to handle exceptions. The code that can possibly throw an exception is put inside the `try` block and the code to handle the exception is put inside the `catch` block.

    ```
    try {
      var result = 12 ~/ 0;
      print('The result is $result');
    } catch(e) {
      print('An error occurred: $e');
    }
    ```

2. **on clause**: If the exception type is known, use an `on` clause to catch it.

    ```
    try {
      var result = 12 ~/ 0;
      print('The result is $result');
    } on IntegerDivisionByZeroException {
      print('Cannot divide by zero');
    }
    ```

3. **finally clause**: Whether an exception is thrown or not, the `finally` clause is always executed.

    ```
    try {
      var result = 12 ~/ 0;
      print('The result is $result');
    } catch(e) {
      print('An error occurred: $e');
    } finally {
      print('This is the finally clause and is always executed.');
    }
    ```

Remember, proper error handling is an important part of writing robust code.
