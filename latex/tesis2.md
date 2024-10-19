---
layout   : page
title    :  Plantilla para tesis en LaTeX
categoria: latex
date     : 2024-10-19 16:00:00 -0600
# Formato de tesis en LaTeX
---

# Este minitutorial te ayudará a utilizar la plantilla de tesis en formato LaTeX que utilizamos tanto para la Maestría en Ciencias de la Computación como para el Doctorado.

#### <strong>Descarga:</strong> [plantilla_tesis2.zip]({{ site.baseurl }}{% link /assets/files/latex/plantilla_tesis2.zip %}) &nbsp; ｜ &nbsp;  <strong>Ejemplo:</strong> [Tesis2.pdf]({{ site.baseurl }}{% link /assets/files/latex/Tesis2.pdf %}){:target="_blank"}

---

<br>

La nueva plantilla para la redacción de tu tesis (<mark class="archivo">Tesis.tex</mark>) se basa en los [Lineamientos para la elaboración de la tesis de licenciatura, especialidad, maestría y doctorado](https://gacetajuchiman.ujat.mx/wp-content/uploads/2024/03/anexo-108.pdf){:target="_blank"} de la UJAT, los cuales a su vez siguen la norma APA en su versión 7: <https://normas-apa.org>{:target="_blank"}.


## 1.  Archivo principal

El archivo <mark class="archivo">Tesis.tex</mark> es el más importante, pues "incluye" los archivos .tex adicionales de cada capítulo (como veremos más adelante).

Pero vamos a describir cada sección del archivo principal para entender su funcionamiento.


### 1.1.  El preámbulo

Todos los paquetes que se importan dentro del preámbulo del documento son esenciales excepto:

~~~latex
% Números de línea para facilitar la revisión
\usepackage{lineno}
~~~

Este paquete sirve para numerar cada línea del documento y así facilitar su revisión. En caso de que quieras eliminar estas guías deberás remover esta instrucción y también eliminar el comando `\linenumbers` dentro del cuerpo del documento.

En el documento encontrarás varios paquetes comentados. LaTeX cuenta con cientos (miles) de paquetes para multitud de usos, pero te sugerimos utilizar los que te proponemos. Simplemente descomentalos y listo.

La configuración global del documento de acuerdo con el formato APA es:

~~~latex
\usepackage{helvet}
\renewcommand{\familydefault}{\sfdefault}
\usepackage[doublespacing]{setspace}
\usepackage{indentfirst}
\usepackage{csquotes}
\usepackage{geometry}
\geometry{
	top=2.54cm,
	left=2.54cm,
	right=2.54cm,
	bottom=2.54cm
}
~~~

Aquí establecemos los márgenes, tipografía, sangría y el doble espacio entre líneas.

### 1.2.  Datos del proyecto

Hemos creado una serie de comandos para definir los elementos que aparecerán en la portada de tu protocolo. Los nombres de los comandos son muy descriptivos, simplemente reemplaza el texto de ejemplo por tu información. Por ejemplo:

- `\newcommand{\Titulo}{}` sirve para definir el título de tu tesis.
- `\newcommand{\Autor}{}` aquí va tu nombre completo.
- `\newcommand{\Director}{}` El nombre de tu director(a) de tesis.
- etcétera.


## 2.  Portada

Los datos de la portada se cargan automáticamente de los datos del proyecto que capturaste en el archivo principal. En caso de que no tengas codirector entonces deberán editar el archivo (<mark class="archivo">Portada.tex</mark>) y comentar (o eliminar) esta sección tanto en la portada a color como en la portada con fondo blanco:

~~~latex
\vfill
EN CODIRECCIÓN:

{\bfseries\MakeUppercase\Codirector}
~~~


## 3. Contenido de la tesis

Como te habrás dado cuenta, hay un montón de archivos .tex en el directorio. Aparte de los ya mencionados <mark class="archivo">Tesis.tex</mark> y <mark class="archivo">Portada.tex</mark> tenemos:

* <mark class="archivo">Declaracion-autoria.tex</mark>: Documento obligatorio que se llena con los datos del proyecto que capturaste en el archivo principal. No olvides firmarlo al final.

* <mark class="archivo">Oficio.pdf</mark>: Es el oficio de impresión de tesis que expide el Director de la División una vez concluído todo el rollo de revisión. Se incluye el PDF tal cual en el documento de tesis con el comando `\includepdf[pages=-]{Oficio}`.

* <mark class="archivo">Cesion-derechos.tex</mark>: Documento obligatorio que igual se rellena automáticamente con los datos introducidos en el archivo principal. Lo deben firmar tanto tú como tu director(a) y codirector(a) de tesis. En caso de que no tengas codirector(a) deberás editar incluir como segundo testigo a la persona que más confianza le tengas.

* <mark class="archivo">Resumen.tex</mark>: Aquí debes colocar el resumen de toda tu tesis en UNA SOLA PÁGINA. También deberás agregar de 3 a 5 palabras clave.

* <mark class="archivo">Cap1-Generalidades.tex</mark>: En este archivo vas a colocar la información de tu protocolo, como el Planteamiento del problema, los Objetivos, etcétera.

* <mark class="archivo">Cap2-Marcos.tex</mark>: Incluye el marco teórico, marco conceptual, marco tecnológico.

* <mark class="archivo">Cap3-Modelo.tex</mark>: Ahora sí viene lo bueno. En este capítulo viene tu propuesta de tesis, por lo que título será diferente para cada estudiante.

* Importante: Si requieres más capítulos para detallar tu investigación, colócalos
aquí. Puedes tener tantos capítulos como sean necesarios, el chiste es describir a
detalle tu investigación.

* <mark class="archivo">Cap4-Resultados.tex</mark>: P describir tus experimentos aquí.
 También puede cambiar de nombre si así lo consideras (pregunta a tu director(a) de tesis).

* <mark class="archivo">Anexo.tex</mark>: Documento obligatorio en el cual debes colocar de nuevo el título de tu tesis, tu nombre, tu ORCID (regístrate en <https://orcid.org>{:target="_blank"} es súper fácil), copiar de nuevo tooodo el resumen, copiar también las palabras clave y al final dejar la leyenda _"En la siguiente página se muestran las referencias"_. Esto es un rollo de Bibliotecas que no te debe importar.

* <mark class="archivo">Cap5-Conclusiones.tex</mark>: Capítulo obligatorio
que no necesito explicarte.

Ahora bien, lo interesante de este embrollo es que cada uno de los archivos mencionados
se "insertan" dentro del archivo principal (o sea dentro de <mark class="archivo">Tesis.tex</mark>)
de la siguiente manera:

~~~latex
%%%%%%%%%%%%%%%%%%%%%%%%% CAPÍTULOS AQUÍ %%%%%%%%%%%%%%%%%%%%%%%%%
\clearpage
\include{Resumen}
\include{Abstract}

\setcounter{page}{1}
\pagenumbering{arabic}
\include{Cap1-Generalidades}
\include{Cap2-Marcos}
\include{Cap3-Modelo}
\include{Cap4-Resultados}
\include{Cap5-Conclusiones}
~~~

Si te das cuenta, el comando `\include{}` inserta el archivo en cuestión (sin la 
extensión .tex), lo que permite tener mejor organizado nuestro documento.

Puntos importantes:

- Si quieres cambiar el nombre de alguno de los archivos, ¡no olvides cambiar el nombre
dentro de su respectivo `\include{}`!
- En el caso de Güindows no importan las mayúsculas/minúsculas en los nombres de archivo,
¡pero en plataformas Linux/Unix sí!


## 4.  Referencias

El formato de referencias sigue el estándar APA. Para poder formatear nuestras referencias usando este estándar es necesario importar el paquete BibLaTeX e importar inmediatamente su archivo de referencias:

~~~latex
\usepackage[style=apa,backend=biber]{biblatex}
\addbibresource{Referencias.bib}
~~~

El archivo <mark class="archivo">Referencias.bib</mark> incluirá todas la bibliografía consultada.

Sé cuidadoso al agregar nuevas entradas a tu archivo archivo de referencias, ya que <code>biber</code> es muy sensible a los errores de sintaxis.

Para citar tienes 2 opciones:

**Cita narrativa**. Es conocida como cita basada en el autor porque se incluye al comienzo de una frase. El nombre del autor se incorpora al texto como parte de la oración y el año sigue entre paréntesis. Ejemplo:

> García-López et al., (2023) developed a software called JMetaBFOP...

La cual en LaTeX quedaría: `\cite{softwarex2023} developed a software called JMetaBFOP \dots`.

**Cita parentética**. En este caso el nombre del autor y la fecha de publicación aparecen entre paréntesis y generalmente se colocan al final de la oración. Ejemplo:

> JMetaBFOP is a tool for solving global optimization problems (García-López et al., 2023)

Para ello hemos creado el comando `\newcommand{\citep}[1]{(\cite{#1})}` para encerrar la cita textual entre paréntesis. Utilizálo como un `\cite` normal: `JMetaBFOP is a tool for solving global optimization problems \citep(softwarex2023)`.

En este caso la referencia es:

~~~bibtex
@article{softwarex2023,
  author = {García-López, Adrian and Chávez-Bosquez, Oscar and Hernández-Torruco, José and Hernández-Ocaña, Betania},
  title  = {JMetaBFOP: A tool for solving global optimization problems},
  journal= {SoftwareX},
  volume = {23},
  year   = {2023},
  doi    = {10.1016/j.softx.2023.101452} 
}
~~~

No olvides colocar el comando `\printbibliography` para imprimir la lista de refencias. Así lo pide BibLaTeX.


## 5.  Imágenes

Finalmente, en el directorio <mark class="archivo">/img</mark> van a colocar las imagénes que incluirá su documento. La instrucción `\graphicspath` le indica a LaTeX que todas las imágenes estarán en este directorio, así que al momento de incluir una figura simplemente escribimos el nombre del archivo sin necesidad de especificar el directorio que la contiene:

~~~latex
  \includegraphics[width=0.7\textwidth]{ia}
~~~


## 6.  Anexos

Es posible agregar anexos, apéndices, u otros archivos de la misma manera
que los capítulos mencionados:

~~~latex
\include{Anexos}
~~~

Agregar esta línea justo después de la sección de Referencias. Obviamente debes
crear el archivo <mark class="archivo">Anexos.tex</mark> con la información
correspondiente.


## 7.  Configuración del Entorno de Desarrollo

Para facilitar la compilación de tu documento, revisa las opciones de tu editor de LaTeX favorito acerca de cómo crear un **Proyecto LaTeX**. Esto te servirá para integrar todos los archivos en un mismo proyecto y así trabajar en un archivo, digamos <mark class="archivo">Resumen.tex</mark> y poder compilar toda la tesis sin
tener que abrir el archivo <mark class="archivo">Tesis.tex</mark>.

Sé que suena confuso, pero ya que comiences a trabajar en tu documento te darás cuenta de que si tratas de compilar el archivo <mark class="archivo">Resumen.tex</mark> ¡te saldrá un error por parte del editor porque ese archivo no tiene preámbulo! Tu editor favorito no lo reconocerá como archivo LaTeX y no lo podrá compilar.

El archivo <mark class="archivo">Tesis.tex</mark> sí que tiene preámbulo, así que este compilará sin problemas (a menos que tengas un error en tu código claro está). De todos modos si tienes alguna bronca no dudes en contactarme.

Para complicar más las cosas, una desventaja de usar el formato APA para las referencias es que es incompatible con BibTeX, el estándar de LaTeX para el manejo de referencias. Entonces tenemos que usar <code>biber</code>, que es un paquete adicional que deberán instalar en su equipo.

Otro detalle surge al momento de compilar en cualquier IDE, ya que por default intentará compilar las referencias usando BibTeX. Deberás configurar tu IDE para que las referencias las compile con biber en lugar de BibTeX de acuerdo a las instrucciones mostradas en <https://texwelt.de/fragen/1909/wie-verwende-ich-biber-in-meinem-editor>{:target="_blank"} (la página está en Alemán pero las imágenes son muy descriptivas).

En caso que utilices TeXstudio, el cual es el IDE que vimos en el taller de LaTeX, debes cambiar la siguiente configuración:

![Consola](texstudio.png)


## 8.  Formato Doctorado

Si eres estudiante de DCC entonces te corresponde cambiar el color de fondo de la portada y el grado a obtener. Esto se hace modificando el archivo <mark class="archivo">Portada.tex</mark>:

~~~latex
    \raisebox{-\height}{\includegraphics[width=\paperwidth]{base_morena}}%
~~~

Y en el archivo principal:

~~~latex
\newcommand{\Grado}{Doctorado en Ciencias de la Computación}
~~~

<br>

¡Listo! Ya tienes todo lo necesario para comenzar a escribir tu anteproyecto sin distracciones.
