---
layout: post
title:  "Tips & tricks de Jekyll"
date:   2021-01-19 23:00:00 -0600
categories: jekyll tips
---

> En esta ocasión vamos a aprender unos trucos de Jekyll que nos van a ser muy 
útiles cuando nuestro sitio web comience a crecer.  

## 1. ¿Como vincular las páginas de mi sitio?

Como ya sabemos, nuestro sitio web se crea compilando los archivos Markdown
para así crear las páginas HTML. Entonces surge la pregunta: ¿como vinculamos
una página que aún no existe?

Para ello utilizamos Liquid, el lenguaje de Jekyll, que combinado con Markdown
nos da la siguiente estructura:

<pre>

</pre>

~~~liquid
[post anterior]({% post_url 2021-01-10-bootstrap %})
~~~