# 14. Creating HTTP Service

Vamos a crear nuestro servicio HTTP, que nos va a permitir interactuar con la REST API enviando peticioneds GET. Una vez creado, lo vamos a
registrar como un **Singleton** con `get_it` en la función `_setup`.

## Creando el servicio HTTP

En nuestra carpeta `lib/`, creamos una nueva carpeta llamada `services/` y dentro de ella un nuevo archivo llamado `http_service.dart`. Crearemos
la clase responsable de manejar los envíos de peticiones. Usaremos el cliente `dio`:

```dart
import '../models/app_config.dart';

// Packages
import 'package:dio/dio.dart';
import 'package:get_it/get_it.dart';

class HTTPService {
  final Dio dio = new Dio();
  final GetIt getIt = GetIt.instance;

  String _base_url;
  String _api_key;

  // Constructor
  HTTPService() {
    AppConfig _config = getIt.get<AppConfig>();
    _base_url = _config.BASE_API_URL;
    _api_key = _config.API_KEY;
  }

  // Función responsable de enviar peticiones a la API, va a retornar un Future de tipo Response
  Future<Response> get(String _path, Map<String, dynamic> query) async {
    try {
      String _url = '$_base_url$_path';
      // En lugar de hacer manualmente los query string ('$_base_url$_path?api_key='), dio nos permite pasarlos como un Map<String, dynamic> y se encarga de convertirlo a query string
      Map<String, dynamic> _query = {
        // Los 2 parámetros que siempre son requeridos en nuestas peticiones
        'api_key': _api_key,
        'language': 'en-US',
      };
      // Si el usuario envía más parámetros, agregamos el diccionario de la query al query Map que ya tenemos
      if (query != null) {
        _query.addAll(query);
      }
      // El await es porque es la respuesta de la petición
      return await dio.get(_url, queryParameters: _query);
    } on DioError catch (e) {
      print('Unable to perform get request.');
      print('DioError:$e');
    }
  }
}
```

* La clase `Response` la provee `dio`
* El `_path` es todo lo que va despues de _base_url y no incluye el query string
* El query string va a ser un argumento opcional de tipo `Map<String, dynamic>`

Ahora, registramos el servicio para que sea accesible por otros servicios presentes en nuestra aplicación.

Nos vamos al `splash_page.dart` y en la función `_setup` agregamos el registro del servicio como un Singleton como hicimos con la clase
`AppConfig`:

```dart
// Services
import '../services/http_service.dart';

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

    // Creamos el Singleton de tipo HTTPService
    getIt.registerSingleton<HTTPService>(
      HTTPService(),
    );
  }
  
}
```

Ahora, corremos el simulador.

* **NOTA:** Es necesario tener listo primero el `AppConfig` para poder crear el `HTTPService` porque el constructor de este último hace uso del primero. Por eso, la manera en que registramos los Singletons es importante.