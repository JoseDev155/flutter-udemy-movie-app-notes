# 5. Creating Flutter Project
## Creando el proyecto

Para crear el proyecto, hacemos:

```bash
flutter create flickd_app
```

Nos devolverá las siguientes instrucciones:

```bash
$ flutter create flickd_app
...
You can find general documentation for Flutter at: https://docs.flutter.dev/
Detailed API documentation is available at: https://api.flutter.dev/
If you prefer video documentation, consider: https://www.youtube.com/c/flutterdev

In order to run your application, type:

  $ cd flick_app
  $ flutter run

Your application code is in flick_app\lib\main.dart.
```

## Versión de Flutter

Lo hacemos con:

```bash
flutter --version
```

* **Versión con la que se hizo el proyecto de Udemy:** `2.0.4`
* Mi versión: `3.41.2`

## Abrir el proyecto

En MacOs, abrimos el directorio del proyecto con:

```bash
open .
```

En Windows:

```powershell
start .
```

Y lo arrastramos a VS Code.

## Extensiones

Antes de manipular el proyecto, vamos a instalar algunas herramientas para ayudarnos con el desarrollo en Flutter:

* **Dart**, de *Dart Code*

Luego, debemos seleccionar un dispositivo para nuestra aplicación de Flutter y la pongamos en marcha con **Run** > **Start Debugging**.

Entoncesm nos vamos a la parte inferior de VS Code, y le damos en **Select a device to use**.

## Iniciando la aplicación

Le damos en **Run** > **Start Debugging** > **Dart & Flutter**.

## Cambios en la aplicación

En `lib/main.dart` cambiamos el `title` y `home`:

```dart
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter',
      theme: ThemeData(
        // This is the theme of your application.
        //
        // TRY THIS: Try running your application with "flutter run". You'll see
        // the application has a purple toolbar. Then, without quitting the app,
        // try changing the seedColor in the colorScheme below to Colors.green
        // and then invoke "hot reload" (save your changes or press the "hot
        // reload" button in a Flutter-supported IDE, or press "r" if you used
        // the command line to start the app).
        //
        // Notice that the counter didn't reset back to zero; the application
        // state is not lost during the reload. To reset the state, use hot
        // restart instead.
        //
        // This works for code too, not just values: Most code changes can be
        // tested with just a hot reload.
        colorScheme: .fromSeed(seedColor: Colors.deepPurple),
      ),
      home: const MyHomePage(title: 'Flickd'),
    );
  }
}
```

Y le damos en **Save and Hot Reload**.