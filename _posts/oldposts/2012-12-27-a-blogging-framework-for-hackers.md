---
layout: post
category: Blogging
tags: [jekyll, github, wordpress]
title: A blogging framework for hackers
author: andresmoschini
---

Estaba escribiendo mi segundo post de la serie sobre mi self-training, pero me siento raro con WordPress. No me siento cómodo escribiendo en su editor wysiwyg; el resaltado de código es feo; hasta ahora ninguno de los templates que pusimos me resultó agradable; quise pegar texto que escribí en markdown o html y me lo rompió. Si no tenemos hosting propio no tenemos control sobre el javascript, css ni podemos instalar plugins.

Este es un blog de desarrolladores de software, deberíamos utilizar un blog engine hecho para nosotros.


_GitHub Pages_ parece ideal: tenemos hosting gratis, git, markdown, resaltado de código, etc. En su momento yo lo había descartado porque no permitía comentarios, pero eso se resuelve con [Disqus](http://disqus.com/).

Otra opción es [Octopress](http://octopress.org/), pero necesitaríamos hosting (Update: funciona con GitHub, pero el build del sitio se realiza manualmente).

Algunos ejemplos de blogs sobre GitHub Pages:

* [Another developer blog](http://erjjones.github.com/blog/How-I-built-my-blog-in-one-day/) ([sources](https://github.com/erjjones/erjjones.github.com/blob/master/_posts/2012-03-08-How-I-built-my-blog-in-one-day.markdown))
* [Alex Rothenberg](http://www.alexrothenberg.com/2011/01/27/moved-blog-to-jekyll-and-github-pages.html) ([sources](https://github.com/alexrothenberg/alexrothenberg.github.com/blob/master/_posts/2011-01-27-moved-blog-to-jekyll-and-github-pages.md))

Más lindo está [Pixel-in-Gene](http://blog.pixelingene.com/2011/09/switching-to-the-octopress-blogging-engine/), construido sobre _Octopress_, pero no parece tener nada interesante que no se pueda hacer con Jekill y GitHub Pages.

**¿Ustedes que opinan? ¿Conocen otras opciones?**