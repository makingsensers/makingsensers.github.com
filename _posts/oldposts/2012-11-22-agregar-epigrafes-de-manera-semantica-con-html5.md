---
layout: post
category: HTML5
title: Agregar epígrafes de manera semántica con HTML5
author: lisandromartinez
---

Actualmente cuando queremos ponerle el epigrafe al pie una imagen (caption) haríamos algo así

{% highlight html %}
<img src="path/a-la/imagen" alt="Acerca de la imagen" /> 
<p>Breve descripción de lo que hay en la imagen</p>
Esta forma de hacerlo no dejaba asociado de manera semántica la imagen a su epígrafe.
Pero hoy con HTML5 y los elementos figure y figcaption se puede hacer de la siguiente manera.
{% endhighlight %}

{% highlight html %}
<figure> 
   <img src="path/to/image" alt="About image" /> 
   <figcaption> 
      <p>This is an image of something interesting. </p> 
   </figcaption> 
</figure> 
{% endhighlight %}

Para ver el soporte que tiene en los navegadores podés checkearlo <http://caniuse.com/#search=figurea>
