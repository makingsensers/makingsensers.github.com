---
layout: post
category: Self-Training / News at a glance
title: jquery-tmpl (templates)
author: leoslopez
tags: [javascript, jquery-tmpl, templates]
---

### jQuery plug-in: [jquery-tmpl](http://api.jquery.com/category/plugins/templates/)

_**Aclaración:** Es conveniente aclarar que el equipo de jQuery ha decidido no hacer uso de este plugin ya que no está siendo activamente desarrollado o mantenido desde hace un tiempo ya. Cuando se comenzó a utilizar en el self training no se tenía conocimiento de esto pero de todos modos, para el uso que se le dió, fue útil y funcionó correctamente._

### Uso en News At A Glance

(*) [News at a Glance en GitHub](https://github.com/leoslopez/Account-At-A-Glance-App)

#### Situación planteada

Se necesitaba poder contar con templates para los diferentes tamaños de ’tiles’ que debía mostrar, y manejar, la aplicación (small, medium y large) para los diferentes tipos de información mostrada (noticias, equipos y videos publicitarios)

#### Resolución usando _jquery-tmpl_ plugin

* [Descargar](http://ajax.aspnetcdn.com/ajax/jquery.templates/beta1/jquery.tmpl.min.js) e incluir en el proyecto el plugin:

{% highlight html %}
<script src="@Url.Content("~/Scripts/Libs/jQuery.tmpl.min.js")" type="text/javascript"></script>
{% endhighlight %}

* Agregar un archivo html para cada tipo de información a mostrar (noticias, equipos, videos). En nuestro caso, para las noticias, se agregó `News.html`.
* Dentro de cada archivo incluir los 3 templates, 1 para cada tamaño de tile considerado: _small_, _medium_ y _large_. El tag principal del template debe tener la siguiente forma:

{% highlight html linenos %}
<!-- template para noticia tamaño small -->
<script id="NewsTemplate_Small" type="text/x-jquery-tmpl">
{% endhighlight %}

* Ahora, usando `$("#myTemplate").tmpl([data])` se indica que el **template** correspondiente se bindeará con determinada **data** (puede ser algún JavaScript type, incluyendo `Array` u `Object`). En la app:

{% highlight js %}
var template = $('#' + tileName + 'Template_' + size); //se obtiene el template
template.tmpl(data); //se bindea la data correspondiente
{% endhighlight %}

{% assign _each = '{{each}}' %}
{% assign _if = '{{if}}' %}
{% assign _else = '{{else}}' %}
{% assign _html = '{{html}}' %}
{% assign _tmpl = '{{tmpl}}' %}
{% assign _wrap = '{{wrap}}' %}

* Para identificar los valores a tener en cuenta al momento de renderizar la **data** sobre el **template** se debe considerar la siguiente sintaxis en la definición del template: `<span id="spNewsSource">${Source}</span>`. Con el template tag: `${Source}` se indica que la **data** pasada por parametro tendrá una property llamada `Source` con un value que será renderizado sobre el `<span>` en cuestión. **Se puede bindear de esta forma ya sea el value de un span como la property `ref` en un anchor `<a id="lnkNews" href="${Url}"`, el source de una imagen, los ids de elementos html, etc**. Ver documentación para los varios template tags: [`${}`](http://www.jquerysdk.com/api/template-tag-equal), [`{{_each}}`](http://www.jquerysdk.com/api/template-tag-each), [`{{_if}}`](http://www.jquerysdk.com/api/template-tag-if), [`{{_else}}`](http://www.jquerysdk.com/api/template-tag-else), [`{{_html}}`](http://www.jquerysdk.com/api/template-tag-html), [`{{_tmpl}}`](http://www.jquerysdk.com/api/template-tag-tmpl) [`{{_wrap}}`](http://www.jquerysdk.com/api/template-tag-wrap).

* El método `$.tmpl()` retorna una jQuery collection y es diseñado para encadenar con `.appendTo`, `.prependTo`, `.insertAfter` or `.insertBefore`, como en este ejemplo: `$.tmpl("<li>${Name}</li>",{"Name" : "John Doe"}).appendTo("#target")`. En la app, el valor retornado por este método, se utilizó de la siguiente manera: `tileDiv.html(template)` (Para el `div` del tile en cuestión se define la property `html` usando el **template**).

#### Conclusión

El plugin permitió una gran comodidad y facilidad para mostrar, bindear y manejar templates previamente definidos sobre los cuales debía mostrarse diferente información, dependiendo del tamaño del template, de manera dinámica (en el momento de la obtención de la noticias).