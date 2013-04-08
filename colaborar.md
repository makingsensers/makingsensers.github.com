---
layout: page
title: Colaborar
header: Colaborar en makingsensers.github.com
group: navigation
---
{% include JB/setup %}

Existen diferentes maneras de colaborar con este blog, cualquier _Makingsenser_ está invitado a hacerlo como mejor le parezca. Es requisito tener una cuenta de GitHub (y estar logueado). 

### Crear un post desde la UI web de GitHub

Ingresando a [la carpeta `_posts` del repositorio del sitio](https://github.com/makingsensers/makingsensers.github.com/tree/master/_posts) se puede crear un nuevo post.

![Crear un nuevo archivo]({{ BASE_PATH }}/img/pages/colaborar/create-file.png)

#### Nombre de archivo **`(1)`**

El nombre de archivo debe satisfacer el formato `yyyy-mm-dd-titulo-del-post-sin-espacios.ext`, y la extensión dependerá del markup elegido para el contenido: `.html`, `.md` para Markdown, o `.textile` para Textile.

![Escribir el contenido]({{ BASE_PATH }}/img/pages/colaborar/write-content.png)

#### Encabezado **`(2)`**

En el encabezado del archivo se incluirá el nombre del _layout_ (en general deberá se `post`), el _title_, _summary_, _author_, _tags_, _category_ e _images_, puede encontrarse un ejemplo en <https://raw.github.com/makingsensers/makingsensers.github.com/master/_posts/2013-01-27-la-prueba-de-la-pizza.md> y para ver más detalles en <https://github.com/mojombo/jekyll/wiki/YAML-Front-Matter>. 

#### Contenido **`(3)`**

El contenido puede ser [Markdown](http://daringfireball.net/projects/markdown/), [Textile](http://txstyle.org/) o directamente HTML. En cualquier caso soporta [Liquid Extensions](https://github.com/mojombo/jekyll/wiki/Liquid-Extensions), por ejemplo para resaltado de sintaxis.

### Pull Request

En caso de no tener permisos aún, la creación de este archivo creará un _pull request_ al repositorio principal del blog, luego de aceptar los cambios intentaremos dar permisos al usuario rápidamente para que este paso no sea necesario en lo sucesivo. 

![Pull Request]({{ BASE_PATH }}/img/pages/colaborar/pull-request.png)

### Post Data

Puede encontrarse más información en:

* <https://github.com/mojombo/jekyll/wiki/Usage>
* <http://jekyllbootstrap.com/lessons/jekyll-introduction.html>

Siéntanse libres de modificar está página, se que no está muy clara ni completa, pero si no la publicaba ahora no lo hacia más.

