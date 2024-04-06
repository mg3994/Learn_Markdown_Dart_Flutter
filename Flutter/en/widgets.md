# Flutter Widgets

Widgets are the building blocks of Flutter applications. Everything in Flutter is a widget, from layout elements like containers and rows to interactive components like buttons and text fields. Flutter provides a wide range of built-in widgets that can be customized and combined to create complex UI layouts.

Widgets in Flutter are lightweight and immutable, allowing for fast and efficient rendering of UI components. Flutter's widget-based architecture enables developers to compose UIs using a hierarchical tree structure, where each widget encapsulates a part of the UI and its corresponding logic. By arranging and styling widgets, developers can create visually appealing and responsive user interfaces for their applications.

# Flutter Widgets: An Overview

Flutter widgets are the building blocks of Flutter applications, allowing developers to create user interfaces and define the structure and behavior of their apps. Widgets can be either visual elements like buttons, text inputs, and images, or structural elements like rows, columns, and containers.

## Introduction to Flutter Widgets

Widgets in Flutter are classified into two main categories: StatelessWidget and StatefulWidget. 

- **StatelessWidget**: These widgets are immutable and do not maintain any state. They are useful for displaying static content that does not change over time.

- **StatefulWidget**: These widgets are mutable and maintain state that can change over time. They are used for interactive elements and components that need to be updated dynamically.

## Commonly Used Widgets

### 1. Text Widget

The Text widget is used to display a single line of text with specified styling, such as font size, color, and alignment.

```

Text(
  'Hello, Flutter!',
  style: TextStyle(fontSize: 20, color: Colors.blue),
)
```

### 2. Container Widget

The Container widget is a versatile widget used for layout and styling. It can contain child widgets and apply properties like padding, margin, color, and border.

```

Container(
  padding: EdgeInsets.all(10),
  margin: EdgeInsets.symmetric(vertical: 20),
  color: Colors.grey,
  child: Text('This is a container'),
)
```

### 3. ElevatedButton Widget

The ElevatedButton widget is a material design button that responds to touches by elevating itself. It is used for actions like submitting forms or navigating to a new screen.

```

ElevatedButton(
  onPressed: () {
    // Action to perform on button press
  },
  child: Text('Submit'),
)
```

### 4. Image Widget

The Image widget is used to display images from various sources, such as assets, network URLs, or memory.

```

Image.network('https://example.com/image.jpg')
```

### 5. ListView Widget

The ListView widget is used to display a scrollable list of children. It is useful for displaying large sets of data that exceed the screen size.

```

ListView(
  children: <Widget>[
    ListTile(title: Text('Item 1')),
    ListTile(title: Text('Item 2')),
    ListTile(title: Text('Item 3')),
  ],
)
```

## Conclusion

Flutter widgets provide a rich set of components and layout options for building beautiful and responsive user interfaces. By understanding the different types of widgets and their properties, developers can create highly customizable and interactive apps in Flutter.
