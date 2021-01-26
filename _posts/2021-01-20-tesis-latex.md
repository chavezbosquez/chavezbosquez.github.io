---
layout: post
title:  "Plantilla para tesis en LaTeX"
date:   2021-01-20 22:29:00 -0600
categories: latex
---

> Este minitutorial te ayudará a utilizar la plantilla de tesis en formato LaTeX
que utilizamos tanto para la Maestría en Ciencias de la Computación como para el
Doctorado

El archivo <mark class="archivo">Tesis.tex</mark> es el más importante, pues "incluye"
los archivos .tex adiciones de cada capítulo (como veremos más adelante).

Pero vamos a describir cada sección del archivo principal para entender su funcionamiento.

## 1. El preámbulo

En general todos los paquetes que importamos en nuestro archivo son
esenciales, exepto:

~~~latex
% Números de línea para facilitar la revisión
\usepackage{lineno}
\linenumbers
~~~

Ya que sirve para numerar cada línea del documento y así facilitar la revisión de la tesis.
Obviamente en la versión final de la tesis debes eliminar estas dos líneas.

<!--
Otros paquetes que en un momento dado podrían ser opcionales son:
* `\usepackage{xcolor}`: En caso de que no requieras colorear texto. 
* ``:
-->

## 2. Portada

La portada de la tesis es un PDF que se crea con otro documento LaTeX. ¿Porqué necesitamos
otro archivo .tex para algo tan simple? ¡Porque no es tan simple!

El punto es que la instrucción:

~~~latex
\includepdf[pages=-]{Portada}
~~~

hace el trabajo (bueno casi).

Lo que debemos hacer primero primero es editar el archivo <mark class="archivo">Portada.tex</mark>
y cambiar los datos relevantes de nuestra tesis:

~~~latex
% Título de la tesis
\newcommand{\Ptitle}{Modelando la generación de menús nutritivos empleando técnicas de Inteligencia Artificial}  
% Autor
\newcommand{\Pauthor}{Oscar Alberto Chávez Bosquez}
% Grado
\newcommand{\Pdegree}{Doctor en Ciencias de la Computación}
% Director 1
\newcommand{\PadviserA}{Dra. María del Pilar Pozos Parra}
% Director 2
\newcommand{\PadviserB}{}

% Presidente
\newcommand{\PjuryA}{Dr. Francisco Javier Álvarez Rodríguez}
% Secretario
\newcommand{\PjuryB}{Dra. Alejandra Anlehu Tello}
% Vocal
\newcommand{\PjuryC}{Dra. María del Pilar Pozos Parra}
% Agregar más revisores en caso de ser necesario
% \newcommand{\PjuryD}{}

% Cuerpo Académico
\newcommand{\PcuerpoAcademico}{Inteligencia Artificial}

% LGAC
\newcommand{\PlineaGAC}{Representación y Manejo del Conocimiento}

% Fecha
\newcommand{\Pmonth}{Junio}
\newcommand{\Pyear}{2019}
~~~

Nota algo importante: 

* En caso de que tengas un codirector debes anotarlo dentro de
`\newcommand{\PadviserB}{}`.
* Si tienes más revisores en tu tesis (que se convierten
en vocales durante tu examen profesional) entonces debes agregarlos con 
`\newcommand{\PjuryD}{}`, `\newcommand{\PjuryE}{}` y así sucesivamente.

Otro detallito que debes revisar es que si tu revisor es hombre o mujer o son 2 (o más).
En este caso tendrás que buscar esta línea y modificarla acorde:

~~~latex
% Modificar de acuerdo a su caso particular
{Directora\par}
~~~

Finalmente, si agregaste vocales (revisores de tesis) entonces deberás agregarlos
en la sección correspondiente:

~~~latex
% Agregar vocales en caso de ser necesario
& {\bfseries\PjuryD\par} & Vocal \\
& {\bfseries\PjuryE\par} & Vocal \\
~~~

## 3. Contenido de la tesis

Como te habrás dado cuenta, hay un montón de archivos .tex en el directorio. 
Aparte de los ya mencionados <mark class="archivo">Tesis.tex</mark> y
<mark class="archivo">Portada.tex</mark> tenemos:

* <mark class="archivo">Resumen.tex</mark>: Aquí debes colocar el resumen de
toda tu tesis en UNA SOLA PÁGINA.

* <mark class="archivo">Cap1-Generalidades.tex</mark>: En este archivo vas a 
colocar la información de tu protocolo, como el Planteamiento del problema, 
los Objetivos, Etcétera.

* <mark class="archivo">Cap2-Marcos.tex</mark>: Incluye el marco teórico,
marco conceptual, marco tecnilógico.

* <mark class="archivo">Cap3-Modelo.tex</mark>: Ahora sí viene lo bueno. En
este capítulo viene tu propuesta de tesis, por lo que título será diferente
para cada estudiante.

* <mark class="archivo">Cap4-Arquitectura.tex</mark>: Este archivo digamos que
es opcional, porque tal vez todo tu trabajo y aporte "quepa" en el Capítulo 3.
Por otro lado, tal vez necesites más capítulos para detallar tu investigación,
así que puedes agregar tantos como sea necesario.

* <mark class="archivo">Cap5-Resultados.tex</mark>: Este capítulo es obligatorio,
ya que debes describir tus experimentos aquí. También puede cambiar de nombre
si así lo consideras (pregunta a tu director de tesis).

* <mark class="archivo">Cap6-Conclusiones.tex</mark>: Otro capítulo obligatorio
que no necesita explicación. 

Ahora bien, lo interesante de este embrollo es que cada uno de los archivos mencionados
se "insertan" dentro del archivo principal (o sea <mark class="archivo">Tesis.tex</mark>)
de la siguiente manera:

~~~latex
% Obligatorio
\include{Resumen}
% Obligatorio
\include{Cap1-Generalidades}
% Obligatorio (Definir el nombre del capítulo en acuerdo con su director tesis)
\include{Cap2-Marcos}
% Estos capítulos deben ser nombrados por el estudiante y director(es), que de 
% idea del desarrollo de la contribución principal de la tesis del estudiante.
% La contribución del estudiante podría ocupar más de un capítulo, en cuyo caso 
% los capítulos siguientes se reenumerarán.
\include{Cap3-Modelo}
\include{Cap4-Arquitectura}
% Obligatorio
\include{Cap5-Resultados}
% Obligatorio
\include{Cap6-Conclusiones}
~~~

Si te das cuenta, el comando `\include{}` inserta el archivo en cuestión (sin la 
extensión .tex), lo que permite tener mejor organizado nuestro documento.

Si quieres cambiar el nombre de alguno de los archivos, ¡no olvides cambiar el nombre
dentro de su respectivo `\include{}`!

## 4. Referencias

Las referencias las incluimos de la manera clásica:

~~~latex
\bibliographystyle{plain}
% Nombre del archivo de referencias (colocar sin extensión .bib)
\bibliography{Tesis}
~~~

Y para ello tenemos el archivo <mark class="archivo">Tesis.bib</mark>.

## 5. Anexos

Es posible agregar anexos, apéndices, u otros archivos de la misma manera
que los capítulos mencionados:

~~~latex
\include{Anexos}
~~~

Agregar esta línea justo después de la sección de Referencias. Obviamente debes
crear el archivo <mark class="archivo">Anexos.tex</mark> con la información
correspondiente.

## 6. Fin

Recuerda agregar la parte de Justificación que te pidió Torruco, aunque no aparezca
en la plantilla. Creemos que es importante para el CONACYT.

Para facilitar la compilación de tu documento, revisa las opciones de tu editor
de LaTeX favorito acerca de cómo crear un **Proyecto LaTeX**. Esto te servirá
para integrar todos los archivos en un mismo proyecto y así trabajar en un arhivo,
digamos <mark class="archivo">Resumen.tex</mark> y poder compilar toda la tesis sin
tener que abrir el archivo <mark class="archivo">Tesis.tex</mark>.

Sé que suena confuso, pero ya que comiences a trabajar en tu documento te darás
cuenta de que si tratas de compilar el archivo <mark class="archivo">Resumen.tex</mark>
¡te saldrá un error por parte del editor porque ese archivo no tiene preámbulo!
Tu editor favorito no lo reconocerá como archivo LaTeX y no lo podrá compilar.

El archivo <mark class="archivo">Tesis.tex</mark> sí que tiene preámbulo, así que este
compilará sin problemas (a menos que tengas un error en tu código claro está). De
todos modos si tienes alguna bronca no dudes en contactarme.
