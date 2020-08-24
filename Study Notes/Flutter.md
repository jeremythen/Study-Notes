



```dart

// To show an image from the web.
NetworkImage("url")

// Or from the assets:
AssetImage("name.jpg")

```

In pubspec.yaml, uncomment assets to use images. - images/


Dynamic type in Dart
```dart
dynamic b = 5;
```

const name1 = getName();
final name2 = getName();
    
name1 = "Whatever";
name2 = "Whatever2";


Column(
      mainAxisAlignment: MainAxisAlignment.spaceBetween,
      crossAxisAlignment: CrossAxisAlignment.stretch,


Custom theme.
```dart
MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(primaryColor: Colors.red, accentColor: Colors.purple, scaffoldBackgroundColor: Colors.blue,),
      home: MyHomePage(title: 'Flutter Demo Home Page'),
      
    );
```

```dart

Color(0xFF0A9E21)


theme: ThemeData.dark().copyWith(
        primaryColor: Color(0xFF0A0E21),
        textTheme: TextTheme(
          bodyText1: TextStyle(
            color: Color(0xFFFFFFFF),
          ),
        ),
      ),


// To give the button a personal theme.
floatingActionButton: Theme(
        data: ThemeData(accentColor: Colors.purple),
        child: FloatingActionButton(
          onPressed: () {},
          tooltip: 'Hello',
          child: Icon(Icons.add),
        ),
      ),



```


GestureDetector is a Widget to detect any gesture like press, drag, etc.


Statefull widget have life cycle methods like:

```dart

@override
void initState() {
  super.initState();
}

@override
void deactivate() { // This is like the destroy method.
  super.deactivate();
}

```

Null Aware Operator

someVariable ?? etc


Importing a package as:

```dart
import 'package:http/http.dart' as http;

http.get(url);

```

For in loop

```dart

for(int myNum in myNumbers) {

}

```

There are mixing in dart: MyClass with MyMixing
mixin MyMixin.

There is no interface in dart, just abstract classes.

import 'package:etc.dart' show SpecificClass

