# 10. Create Splash Page | Part 1

Vamos a empezar a crear el Splash Screen para nuestra aplicación de Flutter.

## Lógica

La manera en que va a funcionar es que en lugar de tener 2 pantallas diferentes, vamos a tener 2 aplicaciones diferentes.

Vamos a crear una nueva splash app y esta va a inicializar las cosas dentro de ella. Cuando haga eso, vamos a remover la aplicación y crear
una nueva aplicación usando the `runApp()` function para abri la nueva aplicación.

## Construyendo el Splash Screen

La primera cosa que haremos en el `main.dart` es quitar toda la clase `MyApp` y vamos a crear la clase `SplashScreen`.

Pero para mantener la convención de nombre, la llamaremos `SplashPage`, y pondremos el código dentro de `pages/splash_page.dart`:

```dart
// Packages
import 'package:flutter/material.dart';

class SplashPage extends StatefulWidget {
  // Se llama una vez que la inicialización se ha completado
  final VoidCallback onInitializationComplete;
  
  // Constructor
  const SplashPage({
    Key key,
    required this.onInitializationComplete,
  }) : super(key: key); // Método super para pasar el key al widget padre

  // Función que crea el estado del widget
  @override
  State<StatefulWidget> createState() {
    return _SplashPageState();
  }
}

// Clase que representa el estado del SplashPage
class _SplashPageState extends State<SplashPage> {
  @override
  Widget build(BuildContext context) {
    return null;
  }
}
```

Y el `main.dart` se va a ver así:

```dart
import 'package:flutter/material.dart';

// Pages
import '../pages/splash_page.dart';

void main() {
  runApp(
    SplashPage(key: UniqueKey(), onInitializationComplete: () => null),
  );
}
```