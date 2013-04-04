---
layout: post
image: /img/posts/2013-01-21-my-menu-invitacion.jpg
category : 
tags : 
title: Programando Arkanoid - Parte 1
author: jraimondi
---

Haciendo ya mucho que no trabajaba en JavaScript sin la utilización de ningún framework, me propuse crear algo simple que a la vez fuera divertido. Pensé en algunas opciones y la ganadora fue un juego de [Arkanoid](http://en.wikipedia.org/wiki/Arkanoid), (que, ahora me entero, es [una de las tantas copias del Breakout](http://en.wikipedia.org/wiki/Breakout_clones), y para mí el nombre original siempre fue Arkanoid, en fin).

El resultado final lo pueden ver [aquí](http://randomjs.alphasmanifesto.com/arkanoid-canvas/arkanoid.html) y el código en mi [repositorio de GitHub](https://github.com/AlphaGit/random-javascript), pero no es tanto el resultado sino el viaje lo que fue interesante y **quiero describir las cosas que aprendí en ese camino**.

Vengan y acompáñenme en mi viaje.

## Documentación:

Como todo principiante, o incluso como todo experto que cada tanto necesita verificar el estado de los estándares, la documentación de referencia es importante. Para hacer este pequeño proyecto me basé en algo de mi experiencia previa, y en la documentación disponible en los siguientes sitios:

- [Mozilla Development Network](https://developer.mozilla.org/), impagable, la calidad de la documentación es increíble.
- [WebPlatform.org](http://www.webplatform.org/), acabo de enterarme de este sitio por la clase de juegos HTML5 en Udacity, pero está también muy completa.
- [W3Schools](http://www.w3schools.com/) para refrescar cosas básicas ("¿cómo eran los parámetros de `array.slice`?" y similares)

## El contenedor:

(Lo que escribiré ahora se puede [ver en el commit 90e6…4f7abd9](https://github.com/AlphaGit/random-javascript/commit/90e6540100631e1a3ae590c3bde4a21b74f7abd9).)

