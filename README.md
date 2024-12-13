# Flutter Project Setup with Very Good CLI and GetX

This guide outlines how to set up a Flutter project using **Very Good CLI** for project organization and **GetX** for state management. Combining these tools ensures a scalable and maintainable project structure while leveraging the simplicity of GetX.

---

## Prerequisites
- [Flutter SDK](https://flutter.dev/docs/get-started/install)
- [Very Good CLI](https://verygood.ventures/blog/introducing-the-very-good-cli)
  ```bash
  dart pub global activate very_good_cli
  ```
- Familiarity with GetX: [GetX Documentation](https://pub.dev/packages/get)

---

## Project Setup

### 1. Create a New Flutter Project with Very Good CLI
```bash
very_good create my_app
cd my_app
```

This creates a Flutter project with a clean architecture setup, pre-configured for testing and modular development.

### 2. Add GetX to the Project
Open `pubspec.yaml` and add the `get` package:

```yaml
dependencies:
  get: ^4.6.5
```

Install the dependencies:
```bash
flutter pub get
```

---

## Project Structure
The project structure is organized as follows:

```
lib/
├── app.dart                 # Main App Entry
├── counter/                 # Counter Feature Module
│   ├── data/                # Data Layer (e.g., APIs, Models)
│   ├── logic/               # Logic Layer (e.g., GetX Controllers)
│   │   ├── counter_controller.dart
│   ├── view/                # UI Layer (e.g., Screens)
│       ├── counter_page.dart
└── main.dart                # App Runner
```

---

## Using GetX for State Management

### 1. Create a Controller
In the `logic/` folder, create `counter_controller.dart`:

```dart
import 'package:get/get.dart';

class CounterController extends GetxController {
  var count = 0.obs;

  void increment() => count++;
}
```

### 2. Create a UI Page
In the `view/` folder, create `counter_page.dart`:

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';
import '../logic/counter_controller.dart';

class CounterPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final CounterController controller = Get.put(CounterController());
    return Scaffold(
      appBar: AppBar(title: Text('Counter')),
      body: Center(
        child: Obx(() => Text('Count: ${controller.count}')),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: controller.increment,
        child: Icon(Icons.add),
      ),
    );
  }
}
```

### 3. Update the App Entry
In `app.dart`, update the app to include the `CounterPage`:

```dart
import 'package:flutter/material.dart';
import 'counter/view/counter_page.dart';

class App extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'My App',
      home: CounterPage(),
    );
  }
}
```

---

## Running the App

To run the app in development mode:
```bash
flutter run
```

---

## Benefits of Very Good CLI + GetX

### Very Good CLI
- Enforces clean architecture and modular design.
- Pre-configured for testing.
- Scales well for larger teams and projects.

### GetX
- Lightweight and fast.
- Combines state management, dependency injection, and navigation.
- Reduces boilerplate for small to medium-sized projects.

---

## Additional Commands
- Run tests:
  ```bash
  flutter test
  ```
- Analyze code:
  ```bash
  flutter analyze
  ```
- Format code:
  ```bash
  flutter format .
  ```

---

## References
- [Very Good CLI Documentation](https://verygood.ventures/blog/introducing-the-very-good-cli)
- [GetX Package](https://pub.dev/packages/get)
