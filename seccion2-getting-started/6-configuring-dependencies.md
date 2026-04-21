# 6. Configuring Dependencies

Vamos a configurar nuestras dependencias en el archivo `pubspec.yaml` y estas dependencias están en diferentes paquetes que vamos a estar usando
en el desarrollo de nuestra aplicación.

No hay muchos paquetes que usaremos.

Las **dependencias de desarrollo** (*dev_dependencies*) no se incluyen en la aplicación final.

## Dependencias

La primera cosa que agregaremos es **Riverpod**, que es una librería de manejo de estado.

Usaremos **Dio** como cliente HTTP para hacer peticiones a nuestra API.

Y finalmente usaremos **get_it**, que nos permite acceder a instancias únicas para diferentes clases definidas dentro de nuestra apliación.

Versiones usadas en el curso:

```yaml
...
dependencies:
  flutter:
    sdk: flutter
  flutter_riverpod: "^0.13.1"
  dio: "^3.0.10"
  get_it: "^7.6.7"
...
```

Versiones actuales:

```yaml
...
dependencies:
  flutter:
    sdk: flutter
  flutter_riverpod: ^3.2.1
  dio: ^5.9.1
  get_it: ^9.2.1
...
```

Y la extensión de Dart debería reconocerlo y actualizarlo automáticamente. Sino, hacemos:

```bash
flutter pub get
```

## assets

Vamos a crear en la raíz del proyecto la carpeta `assets/`. Y dentro crearemos 2 carpetas:

```plaintext
assets/
  config/ # Archivos sensibles no públicos
  images/ # Imágenes estáticas para el desarrollo de nuestra aplicación
```
Dentro de la carpeta `config/`, creamos el archivo `main.json`. Dentro tendremos 3 *keys*:

```json
{
    "API_KEY": "",
    "BASE_API_URL": "",
    "BASE_IMAGE_API_URL": ""
}
```

Regresamos al `pubspec.yaml` y le diremos a Flutter que cargue la carpeta `assets/` y haga los archivos disponibles para la aplicación.
Descomentamos la sección de `assets` y cambiamos así:

```yaml
flutter:
  ...
  # To add assets to your application, add an assets section, like this:
  assets:
    - assets/config/
    - assets/images/
  ...
```

Le damos a **Save and Hot Reload**, y **Restart**.