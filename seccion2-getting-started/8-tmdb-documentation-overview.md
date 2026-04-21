# 8. TMDB Documentation Overview

Vamos a tomar una vista rápida de la documentación provista por la API de [TMDB Docs](https://developer.themoviedb.org/docs/getting-started).

Y vamos a inspeccionar los *endpoints* que vamos a usar para traer los datos.

## Movies

Es la primera sección que vamos a inspeccionar. Está en **MOVIES** > **Get Details**.

>En la sección actual, debemos seleccionar la opción **<> API Reference** > **MOVIES** > **Details**

**Get Popular:**

```
GET /movie/popular
```

**Get Upcoming:**

```
GET /movie/upcoming
```

Las repuestas de **Get Popular** y **Get Upcoming**, son las mismas (actualmente se encuentran en la sección **MOVIE LISTS**).

Después del curso, podríamos extender las funcionalidades. Como implementar **Get Similar Movies**. Esto nos ayudará en nuestro proceso
de desarrollo.

## Imágenes

Sin importar que *endpoint* usemos, las imágenes son retornadas.

Recordemos que copiamos `BASE_IMAGE_API_URL`, y la razón de eso es porque cuando vamos a estar obteniendo la respuesta desde la API actual,
la imagen es provista:

* `poster_path`: Este es un **string**, el nombre seguido de la extensión, con esto tendremos una URL completa