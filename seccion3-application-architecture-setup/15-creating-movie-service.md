# 15. Creating Movie Service

Haremos el mismpo proceso para otro servicio que crearemos, que es el **Movie Service**.

Este servicio nos va a permitir tener acceso a toda la diferente información que requerimos en nuestra aplicación, teniendo películas
populares, estrenos de películas o buscar películas.

## Creando el Movie Service

Vamos a crear la shell del Movie Service y lo vamos a registrar. En otras secciones dónde la vamos a requerir lo que necesitamos, vamos a
codificar la funcionalidad en el servivio y luego usarla a través de la aplicación.

Creamos un nuevo archivo dentro de la carpeta `services/` con el nombre `movie_service.dart`. Y creamos la clase `MovieService` dentro de este archivo:

```dart
// Packages
import 'package:get_it/get_it.dart';

// Services
import '../services/http_service.dart';

class MovieService {
  final GetIt getIt = GetIt.instance;

  HTTPService _http;

  // Constructor
  MovieService() {
    // Accedemos a la instancia de HTTPService mediante GetIt
    _http = getIt.get<HTTPService>();
  }
}
```

Ahora, regresamos al `splash_page.dart` y lo registramos dentro de la función `_setup()` como un Singleton:

```dart
// Services
import '../services/movie_service.dart';

class _SplashPageState extends State<SplashPage> {

  Future<void> _setup(BuildContext _context) async {
    final getIt = GetIt.instance;

    final configFile = await rootBundle.loadString('assets/config/main.json');
    final configData = jsonDecode(configFile);

    getIt.registerSingleton<AppConfig>(
      AppConfig(
        BASE_API_URL: configData['BASE_API_URL'],
        BASE_IMAGE_URL: configData['BASE_IMAGE_URL'],
        API_KEY: configData['API_KEY'],
      ),
    );

    getIt.registerSingleton<HTTPService>(
      HTTPService(),
    );

    // Registramos el MovieService como un Singleton
    getIt.registerSingleton<MovieService>(
      MovieService(),
    );
  }

}
```

>Esto es así porque el `MovieService` depende del `HTTPService`

Recargamos la aplicación para ver que todo funcione.