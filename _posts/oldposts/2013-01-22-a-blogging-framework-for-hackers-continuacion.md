---
layout: post
image: /img/posts/2013-01-22-a-blogging-framework-for-hackers-continuacion.jpg
category : Blogging
tags : jekyll, github, markdown, wordpress
title: A blogging framework for hackers (Continuación)
author: andresmoschini
---

Luego de desahogarme en un [post anterior][], continué investigando y probando opciones de blogs basados en [jekyll][] y GitHub. 

[La idea][] es interesante: preparamos los fuentes jekyll del sitio y los post, luego GitHub se encarga de generar el sitio HTML. Los fuentes de posts son archivos HTML con Liquid o Markdown y tenemos total libertad en cuanto a la estructura del sitio y el contenido. Además, no tenemos que lidiar con esos editores de texto online pseudo WYSIWYG ya que trabajamos con archivos de texto y la publicación la realizamos con nuestro sistema de control de versiones preferido: **Git**.


### Intento 1 - Preparar un sitio desde cero

En principio intenté preparar un sitio desde cero, o copiando otros como el de [Eric Jones][]. Dado mi escaso conocimiento de _Ruby_, _Jekyll_ y _Liquid_, creo que no fue una buena elección ya que la estructura no resultó la mejor y algunos literales como la URL base del sitio quedaron repartidos por todo el código. De cualquier manera, rescaté la experiencia y unos snippets de código que utilicé luego.


### Intento 2 - Octopress

[Octopress][] está muy bien, es muy completo y tiene buena terminación. 

Pero, el sitio no es generado por GitHub sino que cuenta con unos scripts para generarlo localmente. Para un blog personal no me parece una mala opción, pero si son muchos los editores, creo que se vuelve un poco más incomodo. Además, perdemos la posibilidad de postear directamente desde GitHub con la [feature de crear archivos][].

Como en el caso anterior, Octopress será una buena _cantera_ para extraer ejemplos, snippets e ideas para utilizar.


### Intento 3 - Jekyll-Bootstrap

[Jekyll-Bootstrap][] resultó ser la opción elegida. Tiene un diseño modular, con templates y helpers. No está tan pulido como Octopress, pero es un buen punto de partida para comenzar a personalizar el sitio.


### Mi prueba de concepto

El objetivo era que las mejoras en estilos, templates y layout no se mezclen con la instancia del sitio, de manera de que se puedan utilizar en otros blogs.

Preparé un repositorio [Jekyll-Bootstrap-MS][], basado en Jekyll-Bootstrap, con algunas modificaciones y adaptaciones. Es aquí donde se deberían realizar las mejoras y personalizaciones de estilos, templates y layout que puedan reutilizarse.

Por otro lado, creé otro [repositorio][andresmoschini blog sources] para mi [blog personal][andresmoschini blog] basado en el anterior. Aquí publicaré mis posts, realizaré cambios puntuales en el layout e ire mergeando las mejoras realizadas en Jekyll-Bootstrap-MS.

### Para probar Jekyll-Bootstrap-MS desde GitHub

El [branch gh-pages de Jekyll-Bootstrap-MS][] está publicado en
<http://makingsense.github.com/jekyll-bootstrap-ms>. Es posible realizar un [Fork de este repositorio][Fork de Jekyll-Bootstrap-MS] y probarlo con la propia cuenta de GitHub, sin necesidad de descargar nada, utilizando las herramientas provistas por GitHub.

### Para probar Jekyll-Bootstrap-MS localmente en Windows

#### Requistos

##### Cliente Git

Yo utilizó [Git Extensions][] que ya incluye MINGW y Git Bash. 

##### Instalar de Ruby

1. Desde [Ruby Installer][] descargar e instalar la última versión de Ruby.
2. Verificar que Ruby esté en el Path o agregarlo.
3. También desde [Ruby Installer][] descargar el Development Kit, descomprimirlo.
4. Desde _Git bash_ ejecutar:

{% highlight bash %}
$ cd C:/RubyDevKit
$ ruby dk.rb init
$ ruby dk.rb install
{% endhighlight %}

##### Instalar Python (requerido si hay páginas con resaltado de sintaxis)

1. [Descargar Python 2.7][] e instalar
2. Verificar que Python esté en el Path o agregarlo.

##### Instalar Jekyll

Desde _Git bash_ instalar Jekyll: 

{% highlight bash %}
$ gem install jekyll
{% endhighlight %}


#### Descargar Jekyll-Bootstrap-MS

Desde _Git bash_:

{% highlight bash %}
$ git clone https://github.com/MakingSense/jekyll-bootstrap-ms.git
{% endhighlight %}

#### Ejecutar Jekyll

{% highlight bash %}
$ cd jekyll-bootstrap-ms
$ jekyll --server
{% endhighlight %}

Abrir <http://localhost:4000> en el navegador

### Pendiente

Algunas posibles mejoras (ver [board en trello][]):

* Estaría bien agregar los números de línea en los snippets de código
* Definir mejor la estructura por defecto del sitio. Por ejemplo, en lugar de un listado de posts en la página de indice, se podrían mostrar los últimos posts completos y la posibilidad de ver los anteriores.
* Link a la página de GitHub de la cuenta asociada al blog.
* Link al source en GitHub del post o página actual.
* Mejorar la utilización de Twitter Bootstrap, por ejemplo utilizando `fluid rows`
* Personalizar Twitter Bootstrap y los estilos.

### Invitación

Creo que este es el motor ideal para un blog de desarrolladores de software. Espero su feedback, críticas, refutaciones, consultas o _pull requests_ en [Jekyll-Bootstrap-MS][].


	

[post anterior]: /2012/12/27/a-blogging-framework-for-hackers/
[La idea]: http://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html
[jekyll]: http://jekyllrb.com/
[Eric Jones]: http://erjjones.github.com/
[Octopress]: http://octopress.org/
[feature de crear archivos]: https://github.com/blog/1327-creating-files-on-github
[Jekyll-Bootstrap]: http://jekyllbootstrap.com/
[Jekyll-Bootstrap-MS]: https://github.com/makingsense/jekyll-bootstrap-ms
[andresmoschini blog sources]: https://github.com/andresmoschini/andresmoschini.github.com
[andresmoschini blog]: http://andresmoschini.github.com
[branch gh-pages de Jekyll-Bootstrap-MS]: https://github.com/makingsense/jekyll-bootstrap-ms/tree/gh-pages
[Fork de Jekyll-Bootstrap-MS]: https://github.com/MakingSense/jekyll-bootstrap-ms/fork_select
[Git Extensions]: https://code.google.com/p/gitextensions/
[Ruby Installer]: http://rubyinstaller.org/downloads/
[Descargar Python 2.7]: http://www.python.org/getit/
[board en trello]: https://trello.com/board/jekyll-bootstrap-ms/50fd498b591dbec63d0081d1