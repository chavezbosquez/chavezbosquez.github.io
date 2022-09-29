---
layout   : page
title    : Formato de protocolo de investigación en LaTeX
categoria: latex
date     : 2021-09-29 15:00:00 -0600
# Formato de protocolo en LaTeX
---

# Este minitutorial les ayudará a utilizar la plantilla de anteproyecto de tesis en formato LaTeX que utilizamos para la Maestría/Doctorado en Ciencias de la Computación.

#### <strong>Descarga:</strong> [plantilla_protocolo.zip]({{ site.baseurl }}{% link /assets/files/latex/plantilla_protocolo.zip %}) &nbsp; ｜ &nbsp;  <strong>Ejemplo:</strong> [Protocolo.pdf]({{ site.baseurl }}{% link /assets/files/latex/Protocolo.pdf %}){:target="_blank"}

---

<br>

## 1. Portada

El archivo <mark class="archivo">portada.tex</mark> es el primer documento que deberán editar. Los campos a que deben incluir se encuentran resaltados en <span style="color: blue">color azul</span>.

Importante: 

* En caso de que tengan un codirector deberán anotarlo dentro de `\newcommand{\PadviserB}{}`. si solamente tienen un director entonces  deberán eliminar esta instrucción.
* Si tienen más de 3 revisores en su tesis (que se convierten en vocales durante tu examen profesional) entonces deberán agregarlos con `\newcommand{\PjuryD}{}`, `\newcommand{\PjuryE}{}` y así sucesivamente.
* Cuidar el género: Maestro/Maestra, Dr./Dra., Director/Directora/Directores.

Al final deberán revisar el documento fuente y eliminar todo rastro de <span style="color: blue">color azul</span>.

## 2. Documento principal

El archivo <mark class="archivo">Protocolo.tex</mark> contiene las secciones necesarias de su anteproyecto de tesis. Los elementos que deben incluir se encuentran resaltados en <span style="color: blue">color azul</span>.

La instrucción:

~~~latex
\includepdf[pages=-]{portada}
~~~

incluye el PDF de la portada que editaron en el paso anterior.

En general, todos los paquetes que se importan dentro del preámbulo del documento son esenciales excepto:

~~~latex
% Números de línea para facilitar la revisión
\usepackage{lineno}
~~~

En caso de eliminar este paquete tienen que quitar la línea `\linenumbers`, ya que sirve para numerar cada línea del documento y así facilitar la revisión de su documento.

Las referencias se incluyen de la manera clásica:

~~~latex
\bibliographystyle{plain}
% Nombre del archivo de referencias (colocar sin extensión .bib)
\bibliography{referencias}
~~~

Y para ello tenemos el archivo <mark class="archivo">referencias.bib</mark>.

De nuevo, deberán revisar el documento fuente y eliminar todo rastro de <span style="color: blue">color azul</span>.


Finalmente, en el directorio <mark class="archivo">/img</mark> se sugiere que coloquen las imagénes a incluir en su documento.
