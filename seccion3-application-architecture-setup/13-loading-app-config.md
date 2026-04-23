# 13. Loading App Config

Queremos cargar los datos de nuestro `main.json` para que este accesible globalmente dentro de nuestra aplicación.

Lo primero que haremos, es que en nuestro `splash_page.dart`, es crear una función dentro de la calse `_SplashPageState` que cargue los datos de
nuestro JSON:

```dart
import 'dart:convert';

// Packages
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
import 'package:get_it/get_it.dart';

// Model
import '../models/app_config.dart';

class _SplashPageState extends State<SplashPage> {
  // Será asíncrona porque puede tardar un poco en cargar los datos
  Future<void> _setup(BuildContext _context) async {
    // Accedemos la instancia de GetIT que nos va a permitir registrar un Singleton en nuestra aplicación
    final getIt = GetIt.instance;

    // rootBundle es una utilidad de sistema de FLutter que nos permite acceder a nuestros archivos
    final configFile = await rootBundle.loadString('assets/config/main.json');
    // Decodificamos el JSON a un diccionario, para esto necesitamos importar el paquete 'dart:convert' al comienzo de nuestro archivo
    final configData = jsonDecode(configFile);

    // Estructuramos los datos con la clase AppConfig y lo registramos como un Singleton de tipo AppConfig
    getIt.registerSingleton<AppConfig>(
      AppConfig(
        BASE_API_URL: configData['BASE_API_URL'],
        BASE_IMAGE_URL: configData['BASE_IMAGE_URL'],
        API_KEY: configData['API_KEY'],
      ),
    );
  }
  
}
```

* `Singleton`: Es una instancia de una clase que es globalmente accesible en todos lados.

Creamos la clase `AppConfig` dentro de `lib/models/app_config.dart`:

```dart
class AppConfig {
  final String BASE_API_URL;
  final String BASE_IMAGE_URL;
  final String API_KEY;

  AppConfig({this.BASE_API_URL, this.BASE_IMAGE_URL, this.API_KEY,});
}
```

Eliminamos la función `Future.delayed` dentro de nuestro `initState()` y la reemplazamos por la función `_setup` en nuestro `splash_page.dart`:

```dart
class _SplashPageState extends State<SplashPage> {

  @override
  void initState() {
    super.initState();
    // Future.delayed(Duration(seconds: 1)).then(
      // (_) => ,
    // );
    _setup(context).then(
      (_) => widget.onInitializationComplete(),
    );
  }

}
```

Ahora, esto no funcionará porque el proceso de carga es tan rápido que no se muestra el Splash Screen. Para solucionar esto, hacemos:

```dart
@override
void initState() {
  super.initState();
  Future.delayed(Duration(seconds: 1)).then(
    (_) => _setup(context).then(
      (_) => widget.onInitializationComplete(),
    ),
  );
}
```

Ahora, tenemos disponible en nuestra aplicación los datos de nuestro `main.json` de forma global con el paquete `get_it` usándolo como un `Singleton`.

En esiguientes vídeos, veremos como desarrollar la funcionalidad de nuestra función `_setup`, mejorando la lógica de nuestra aplicación y agregando servicios que necesitaremos después.