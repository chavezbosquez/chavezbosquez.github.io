---
layout: post
title:  "Añadiendo Bootstrap 5 a nuestro sitio"
date:   2021-01-10 19:00:00 -0600
categories: jekyll bootstrap
---

> Queremos tener la funcionalidad de [Bootstrap](https://getbootstrap.com) en nuestro sitio.
Esa facilidad de crear columnas, botones con diseño, hermosos paneles...
¿Podemos lograrlo sin quebrarnos la cabeza? Intentémoslo.

## 1. Descarga

Vamos a necesitar los _archivos fuente_ de Bootstrap, así que debemos descargar la versión 
que dice **Download source** desde la página de descargas.

<div class="alert alert-warning" role="alert">
  <strong>Nota:</strong> No sé en que futuro estés leyendo esto, pero al sol de hoy la versión
  más reciente de Bootstrap es la 5.0.0, ¡nuevísima!. Revisa bien las instrucciones para tu
  versión futurista de Bootstrap.
</div>

## 2. Configurar nuestro sitio

El archivo descargado es un comprimido, en mi caso **bootstrap-5.0.0-beta1-dist.zip**. Dentro
encontrarás un directorio llamado **scss**. Todo lo que está ahí dentro es por así decirlo 
el código fuente de Boostrap, y se trata de archivos [**Sass**](https://sass-lang.com),
una especie de [hojas de estilo CSS](https://developer.mozilla.org/es/docs/Web/CSS) con esteroides.

### 2.1. Copiar archivos

Vamos a copiar todo este montón de archivos al directo **_sass** de nuestro sitio. Pero
para mantener organizado nuestro sitio vamos a crear el directorio **bootstrap5** y precisamente
en este nuevo directorio vamos copiar todos los archivos y carpetas.

### 2.2. Crear el archivo **bootstrap.scss**

Ahora vamos a decirle a Jekyll que queremos usar todos estos archivos que recién agreamos a nuestro
sitio. Vamos a crear el archivo **bootstrap.scss** dentro del mismo directorio **_sass** y le agregamos
lo siguiente:

~~~css
/* Requeridos */
@import
  "bootstrap5/_mixins.scss",
  "bootstrap5/_functions.scss",
  "bootstrap5/variables.scss";

/* Estilos deseados */
@import
  "bootstrap5/_grid.scss",
  "bootstrap5/_alert.scss",
  "bootstrap5/_buttons.scss";
~~~

Si observan detalladamente, el primer bloque de archivos corresponden a código que contiene la 
configuración de Bootstrap, mientras que el segundo bloque contiene los componentes que queremos
incluir en nuestro sitio. En este caso me interesa únicamente poder hacer diseños con columnas,
desplegar mensajes de alerta, y darle diseño a mis botones.

¿Porqué solamente importamos estos archivos en lugar de incluir TODA la funcionalidad de Bootstrap?
Lo más sencillo hubiera sido incluir únicamente la línea `@import "bootstrap5/bootstrap"` para así
tener todo el poder de Bootstrap peeero... ¡desconfigura nuestro tema de Jekyll! 

Hagamos una prueba del funcionamiento:

~~~html
<a class="btn btn-primary">Botón</a>
~~~

y deberíamos ver algo como esto:

### 2.3. Editar el archivo **main.scss**

Agregamos nuestro recién creado archivo scss al principal documento de estilo de nuestro sitio,
el cual se encuentra dentro de **assets/main.scss**:

~~~css
@import "bootstrap";
@import "minima";
~~~

¡Voilà! Tenemos la funcionalidad que queremos de Bootstrap sin desconfigurar nuestro sitio.
Dependiendo de los componentes que incluyamos será la funcionalidad extra que tengamos
disponible.

### 3. Conclusión

**Importante**: En el archivo **.gitignore** es necesario comentar/quitar la línea:

~~~bash
_site
.sass-cache
.jekyll-cache
.jekyll-metadata
.gitignore
#vendor
~~~

porque casualmente el directorio `vendor` contiene archivos de Bootstrap, y recordad que **.gitignore** evita que sincronicemos con GitHub los archivos o directorios que en el se enlistan.

¿Cómo descrubrí esto? Pues al momento de hacer _push_ de mi repositorio local a GitHub me llegó un correo con el siguiente mensaje:

<small>
The page build failed for the `master` branch with the following error:

Your SCSS file `assets/main.scss` has an error on line 6: File to import not found or unreadable: vendor/rfs. Load paths: _sass /hoosegow/.bundle/ruby/2.7.0/gems/jekyll-theme-primer-0.5.4/_sass /hoosegow/.bundle/ruby/2.7.0/gems/jekyll-theme-primer-0.5.4/_sass /hoosegow/.bundle/ruby/2.7.0/gems/jekyll-theme-primer-0.5.4/_sass. For more information, see https://docs.github.com/github/working-with-github-pages/troubleshooting-jekyll-build-errors-for-github-pages-sites#invalid-sass-or-scss.
</small>

Entonces supuse que algún archivo de mi sitio local no se había cargado en el servidor, y explorando a detalle el correo podemos ver que menciona un archivo **vendor/rfs**.

### Referencias

Cabe mencionar que no hay mucha información al respecto, ¡y menos en español!. De cualquier
manera aquí van unos artículos en lo que me basé para esta actividad:

- Daniel Sieger (2019). [Creating a Jekyll Bootstrap Template](https://www.danielsieger.com/blog/2019/01/12/creating-jekyll-bootstrap-template.html).
- Andreas Veithen (2016). [Using Bootstrap CSS with Jekyll](https://veithen.io/2015/03/26/jekyll-bootstrap.html).

Para entender un poco la estructura de archivos fuente de Bootstrap:

- The Bootstrap Team (2021). [Learn how to theme, customize, and extend Bootstrap with Sass, a boatload of global options, an expansive color system, and more](https://getbootstrap.com/docs/5.0/customize/overview/).