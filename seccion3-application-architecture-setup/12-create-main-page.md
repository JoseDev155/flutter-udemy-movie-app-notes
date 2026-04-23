# 12. Create Main Page

Vamos a crear la otra página para la aplicación. La cual será la página principal.

Está es l página que nosotros vamos a transferir una vez la inicialización este completada dentro de nuestra `SplashPage`.

## Main Page

Dentro del directorio `pages/`, creamos un nuevo archivo llamado `main_page.dart` y dentro de este agregamos el siguiente código:

```dart
// Packages
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';

// Clase responsable de generar la página principal de la aplicación
// ConsumerWidget viene de las librerías de Riverpod, nos provee otro argumento llamado ScopedReader, el cual nos permite leer los providers que nosotros hayamos creado
class MainPage extends ConsumerWidget {
  
  @override
  Widget build(BuildContext context, ScopedReader watch) {
    return _buildUI();
  }

  Widget _buildUI() {
    // Por ahora, retornamos un Scaffold vacío
    return Scaffold();
  }
}
```

Ahora, en el `main.dart`, vamos a pasar de nuestra `SplashPage` a la otra app.

La función `runApp()`, dentro de la función `onInitializationComplete()` de la `SplashPage`, va a ser reemplazada por el siguiente código:

```dart
import '../pages/main_page.dart';

void main() {
  // Flutter va a ignorar la otra app y va a correr la MainPage()
  runApp(
    SplashPage(key: UniqueKey(), onInitializationComplete: () => runApp(MainPage()))
  );
}

// Definimos la clase actual que va a instanciarse al correr la aplicación con algunos funcionalidades de MaterialApp
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flickd',
      initialRoute: 'home',
      routes: {
        'home': (BuildContext _context) => MainPage(),
      },
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      )
    );
  }
}
```

Ahora, si corremos la aplicación, `MyApp()` no se ejecuta. Esto porque en ningún momento la llama dentro de `SplashPage()`.

La debemos llamar de nuestra clase `State<SplashPage>`:

```dart
class _SplashPageState extends State<SplashPage> {

  @override
  void initState() {
    super.initState();
    // Accedemos a las propiedades de la clase padre, y llamamlos a la función onInitializationComplete, la cual va a ejecutar el código que le pasamos desde el main.dart
    widget.onInitializationComplete();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flickd',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: Center(
        child: Container(
          height: 200,
          width: 200,
          decoration: BoxDecoration(
            image: DecorationImage(
              fit: BoxFit.contain,
              image: AssetImage('assets/images/logo.png')
            ),
          ),
        ),
      ),
    );
  }
}
```

Ahora, tendremos otro error, ya que no hemos proveido un `ProviderScope` para la aplicación.
Los `ConsumerWidget` necesitan acceder a los providers dentro de un contexto de `ProviderScope`.

Debemos incluir algún `ProviderScope`, recomablemente el que se encuentra en `main.dart`:

```dart
// Packages
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';

void main() {
  runApp(
    SplashPage(
      key: UniqueKey(),
      onInitializationComplete: () => runApp(
        // Dentro del ProviderScope, llamamos a MyApp(), el cual es el widget raíz de la aplicación
        ProviderScope(
          child: MyApp()
        ),
      ),
    ),
  );
}
```

Ahora, no tendremos ningún error, pero no veremos el Splash Screen, esto porque el `onInitializationComplete()` del `State` se ejecuta instantáneamente.

Esto se arregla fácilmente, con un delay timer en `splash_page.dart`:

```dart
void initState() {
  super.initState();
  // Delay de 1 segundo para que se vea el Splash Screen, y ejecutamos la función onInitializationComplete en lugar de hacerlo afuera
  Future.delayed(Duration(seconds: 1)).then((_) => widget.onInitializationComplete());
  }
```

## **Extras**

`ScopedReader` está depreacado, en su lugar se recomienda usar `WidgetRef`:

```dart
@override
Widget build(BuildContext context, WidgetRef ref) {
  return _buildUI();
}
```