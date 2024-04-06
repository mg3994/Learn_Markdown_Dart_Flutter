#### io: Input/Output Operations in Dart

In Dart, input/output (I/O) operations are essential for interacting with files, streams, and other input/output devices. Dart provides a rich set of libraries and APIs for performing various I/O operations.

##### File Handling
Dart supports file handling operations such as reading from and writing to files. The `dart:io` library provides classes like `File` and `Directory` for working with files and directories. Developers can perform operations such as reading, writing, copying, and deleting files using these classes.

##### Streams
Dart leverages the concept of streams for handling asynchronous I/O operations. Streams represent sequences of data that are continuously generated or consumed. Dart provides a `Stream` class and various stream transformers to work with asynchronous data.

##### Standard Input/Output
Dart allows interaction with the standard input and output streams. Developers can use methods like `stdin.readLineSync()` to read input from the console and `stdout.write()` to write output to the console.

##### Network Operations
Dart enables network I/O operations through its `dart:io` library. Developers can create client and server applications, perform HTTP requests, and handle network communication using Dart's networking APIs.

By leveraging Dart's I/O capabilities, developers can build powerful applications that interact with files, streams, consoles, and network resources efficiently.

For more in-depth information about input/output operations in Dart, refer to the official Dart documentation and guides.

# Input/Output Operations in Dart

Input/Output (I/O) operations are essential for any programming language as they enable communication with the outside world, such as reading data from files, receiving user input, and printing output to the console. In Dart, there are several mechanisms available for performing I/O operations efficiently.

## Reading Input from the Console

To read input from the console in Dart, you can use the `stdin` stream provided by the `dart:io` library. Here's an example of how to read a line of text from the console:

```
import 'dart:io';

void main() {
  print('Enter your name: ');
  String name = stdin.readLineSync();
  print('Hello, $name!');
}
```

In this example, `stdin.readLineSync()` is used to read a line of text entered by the user from the console.

## Writing Output to the Console

To write output to the console in Dart, you can use the `stdout` object provided by the `dart:io` library. Here's an example of how to print output to the console:

```
import 'dart:io';

void main() {
  stdout.write('Enter your name: ');
  String name = stdin.readLineSync();
  stdout.write('Enter your age: ');
  int age = int.parse(stdin.readLineSync());
  
  print('Hello, $name! You are $age years old.');
}
```

In this example, `stdout.write()` is used to print text to the console without adding a newline character at the end.

## Working with Files

Dart provides classes for working with files and directories in the `dart:io` library. Here's an example of how to read the contents of a text file:

```
import 'dart:io';

void main() {
  File file = File('example.txt');
  if (file.existsSync()) {
    String contents = file.readAsStringSync();
    print('File contents: $contents');
  } else {
    print('File not found.');
  }
}
```

In this example, `File` is used to represent a file, and `readAsStringSync()` is used to read the contents of the file as a string.

## Asynchronous I/O Operations

Dart also supports asynchronous I/O operations using futures and async/await syntax. This allows you to perform I/O operations without blocking the execution of your program. Here's an example of reading a file asynchronously:

```
import 'dart:io';

void main() async {
  try {
    File file = File('example.txt');
    String contents = await file.readAsString();
    print('File contents: $contents');
  } catch (e) {
    print('Error reading file: $e');
  }
}
```

In this example, `await file.readAsString()` is used to asynchronously read the contents of the file.

## Conclusion

In Dart, performing input/output operations is straightforward and efficient, thanks to the built-in libraries and asynchronous support. Whether you need to interact with the console or work with files, Dart provides the necessary tools to handle I/O operations effectively.

