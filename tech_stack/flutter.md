# FLUTTER FORMAL SPECIFICATION 
## 12 PRIMARY FLUTTER KEYWORDS

### 1. **WIDGET** - UI Building Blocks
```dart
// Stateless widget
class UserCard extends StatelessWidget {
  final String name;
  final String email;
  
  const UserCard({required this.name, required this.email});
  
  @override
  Widget build(BuildContext context) {
    return Card(
      child: Padding(
        padding: EdgeInsets.all(16),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(name, style: Theme.of(context).textTheme.headline6),
            SizedBox(height: 8),
            Text(email),
          ],
        ),
      ),
    );
  }
}

// Stateful widget
class Counter extends StatefulWidget {
  @override
  State<Counter> createState() => _CounterState();
}

class _CounterState extends State<Counter> {
  int count = 0;
  
  @override
  Widget build(BuildContext context) {
    return FloatingActionButton(
      onPressed: () => setState(() => count++),
      child: Text(count.toString()),
    );
  }
}
```

### 2. **STATE** - State Management
```dart
// Using setState
class MyApp extends StatefulWidget {
  @override
  State<MyApp> createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  int counter = 0;
  
  void incrementCounter() {
    setState(() {
      counter++;
    });
  }
  
  @override
  Widget build(BuildContext context) {
    return Text('Count: $counter');
  }
}

// Using Provider
class MyProvider extends ChangeNotifier {
  int _count = 0;
  int get count => _count;
  
  void increment() {
    _count++;
    notifyListeners();
  }
}

// Consumer
Consumer<MyProvider>(
  builder: (context, provider, child) {
    return Text('Count: ${provider.count}');
  },
)
```

### 3. **LAYOUT** - Layout Widgets
```dart
// Column
Column(
  mainAxisAlignment: MainAxisAlignment.center,
  children: [
    Text('First'),
    Text('Second'),
    Text('Third'),
  ],
)

// Row
Row(
  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
  children: [
    Icon(Icons.home),
    Icon(Icons.search),
    Icon(Icons.settings),
  ],
)

// Stack
Stack(
  children: [
    Image.asset('background.png'),
    Positioned(
      top: 10,
      left: 10,
      child: Text('Overlay'),
    ),
  ],
)

// GridView
GridView.builder(
  gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
    crossAxisCount: 2,
  ),
  itemBuilder: (context, index) => UserCard(),
)
```

### 4. **NAVIGATION** - Navigation & Routing
```dart
// Navigator.push
ElevatedButton(
  onPressed: () {
    Navigator.of(context).push(
      MaterialPageRoute(builder: (context) => DetailPage()),
    );
  },
  child: Text('Go to Detail'),
)

// Named routes
MaterialApp(
  routes: {
    '/': (context) => HomePage(),
    '/detail': (context) => DetailPage(),
  },
)

// Navigate with name
Navigator.of(context).pushNamed('/detail')
```

### 5. **FORM** - Form Handling
```dart
class MyForm extends StatefulWidget {
  @override
  State<MyForm> createState() => _MyFormState();
}

class _MyFormState extends State<MyForm> {
  final _formKey = GlobalKey<FormState>();
  String name = '';
  
  @override
  Widget build(BuildContext context) {
    return Form(
      key: _formKey,
      child: Column(
        children: [
          TextFormField(
            validator: (value) {
              if (value == null || value.isEmpty) {
                return 'Please enter name';
              }
              return null;
            },
            onSaved: (value) => name = value!,
          ),
          ElevatedButton(
            onPressed: () {
              if (_formKey.currentState!.validate()) {
                _formKey.currentState!.save();
                print('Name: $name');
              }
            },
            child: Text('Submit'),
          ),
        ],
      ),
    );
  }
}
```

### 6. **HTTP** - API Calls
```dart
import 'package:http/http.dart' as http;
import 'dart:convert';

class ApiService {
  Future<List<User>> fetchUsers() async {
    final response = await http.get(
      Uri.parse('https://api.example.com/users'),
    );
    
    if (response.statusCode == 200) {
      List<dynamic> data = jsonDecode(response.body);
      return data.map((u) => User.fromJson(u)).toList();
    } else {
      throw Exception('Failed to load users');
    }
  }
  
  Future<User> createUser(User user) async {
    final response = await http.post(
      Uri.parse('https://api.example.com/users'),
      headers: {'Content-Type': 'application/json'},
      body: jsonEncode(user),
    );
    
    if (response.statusCode == 201) {
      return User.fromJson(jsonDecode(response.body));
    } else {
      throw Exception('Failed to create user');
    }
  }
}
```

### 7. **ASYNC** - Asynchronous Programming
```dart
// FutureBuilder
FutureBuilder<List<User>>(
  future: apiService.fetchUsers(),
  builder: (context, snapshot) {
    if (snapshot.connectionState == ConnectionState.waiting) {
      return CircularProgressIndicator();
    } else if (snapshot.hasError) {
      return Text('Error: ${snapshot.error}');
    } else {
      return ListView.builder(
        itemCount: snapshot.data!.length,
        itemBuilder: (context, index) {
          return UserCard(user: snapshot.data![index]);
        },
      );
    }
  },
)

// Async/await
Future<void> loadData() async {
  try {
    final users = await apiService.fetchUsers();
    setState(() {
      _users = users;
    });
  } catch (e) {
    print('Error: $e');
  }
}
```

### 8. **STORAGE** - Local Storage
```dart
import 'package:shared_preferences/shared_preferences.dart';

class LocalStorage {
  Future<void> saveUser(User user) async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.setString('user', jsonEncode(user));
  }
  
  Future<User?> getUser() async {
    final prefs = await SharedPreferences.getInstance();
    final userJson = prefs.getString('user');
    return userJson != null ? User.fromJson(jsonDecode(userJson)) : null;
  }
}
```

### 9. **THEME** - Theming & Styling
```dart
MaterialApp(
  theme: ThemeData(
    primaryColor: Colors.blue,
    textTheme: TextTheme(
      headline6: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
      bodyText2: TextStyle(fontSize: 14, color: Colors.grey),
    ),
  ),
  home: HomePage(),
)

// Using theme in widget
Text(
  'Title',
  style: Theme.of(context).textTheme.headline6,
)
```

### 10. **ANIMATION** - Animations
```dart
class AnimatedWidget extends StatefulWidget {
  @override
  State<AnimatedWidget> createState() => _AnimatedWidgetState();
}

class _AnimatedWidgetState extends State<AnimatedWidget>
    with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _animation;
  
  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: Duration(seconds: 1),
      vsync: this,
    );
    _animation = Tween(begin: 0.0, end: 1.0).animate(_controller);
    _controller.forward();
  }
  
  @override
  Widget build(BuildContext context) {
    return FadeTransition(
      opacity: _animation,
      child: Text('Fading Text'),
    );
  }
  
  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }
}
```

### 11. **PERMISSION** - Permissions
```dart
import 'package:permission_handler/permission_handler.dart';

Future<void> requestCameraPermission() async {
  final status = await Permission.camera.request();
  if (status.isGranted) {
    // Camera access granted
  } else if (status.isDenied) {
    // Permission denied
  } else if (status.isPermanentlyDenied) {
    // Permission permanently denied, open app settings
    openAppSettings();
  }
}
```

### 12. **TESTING** - Testing
```dart
import 'package:flutter_test/flutter_test.dart';

void main() {
  group('UserCard Widget', () {
    testWidgets('displays user info', (WidgetTester tester) async {
      await tester.pumpWidget(
        MaterialApp(
          home: UserCard(name: 'John', email: 'john@example.com'),
        ),
      );
      
      expect(find.text('John'), findsOneWidget);
      expect(find.text('john@example.com'), findsOneWidget);
    });
    
    testWidgets('button triggers callback', (WidgetTester tester) async {
      bool tapped = false;
      await tester.pumpWidget(
        MaterialApp(
          home: Scaffold(
            body: ElevatedButton(
              onPressed: () => tapped = true,
              child: Text('Tap'),
            ),
          ),
        ),
      );
      
      await tester.tap(find.byType(ElevatedButton));
      expect(tapped, true);
    });
  });
}
```

## BEST PRACTICES
1. Use const constructors
2. Optimize widget rebuilds
3. Use Provider for state management
4. Handle async operations properly
5. Validate user input
6. Test thoroughly
7. Handle errors gracefully
8. Optimize app performance
9. Use proper theming
10. Follow Flutter style guide
