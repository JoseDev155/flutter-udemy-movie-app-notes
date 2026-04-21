# 7. Obtaining API Information

Vamos a obtener nuestro `API_KEY` y `BASE_API_URL` para comunicaeros con la APY y obtener todo de nuestras películas.

La web que usaremos es [TMDB](https://www.themoviedb.org/). Nos vamos a registrar para tener una `API_KEY` gratuita.

## Pasos

* Nos registramos y validamos con una cuenta
* Nos logueamos, vamos a nuestro **Perfil**

### API Key

* Hacemos clic en *nuestro perfil* > **Settings** > **API**
* Aquí vamos a **Request an API key**
* La copiamos de **API Key (v3 auth)** (*Clave de la API*)
* Regresamos a la aplicación y la pegamos en `API_KEY`

### URL Base

* Luego, en **API**, nos vamos a la sección **Documentation** para ver todos los diferentes **endpoints** que tenemos para interatuar
* Una vez entremos a este apartado, veremos la *URL base* principal (actualmente está en **USING THE API** *Append To Response*)

### Imágenes

* Y finalmente, para las imágenes nos vamos a **GETTING STARTED** > **Images** (ahora está en **IMAGES** > **Basics**)
* Y veremos diferentes ejemplos del tipo de URL a usar
* Copiamos el primero y removemos la imagen de ejemplo

>Esto significa que cuando agreguemos un nombre, vamos a formar una URL completa y el tamaño de la imagen que vamos a recibir va a ser el original

## Contenido final del `main.json`

```json
{
    "API_KEY": <API-KEY>,
    "BASE_API_URL": "https://api.themoviedb.org/3",
    "BASE_IMAGE_API_URL": "https://image.tmdb.org/t/p/original/"
}
```

**NOTA:** Las peticiones a la API toman un tiempo en ser verificadas y aceptadas. Pero el 99% de las veces son aprobadas.
Como recomendación, seleccionemos la opción de motivos **Educational** (*Educativos*).