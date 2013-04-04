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

Lo primero y principal, y lo más simple fue setear el HTML y los estilos necesarios. **Todo estará hecho en HTML5 Canvas** y siendo manejado a través de JavaScript, nuestra estructura en el DOM en sí no debería ser demasiado compleja. Sí necesitamos, sin embargo, un documento válido y limpio.

    <!DOCTYPE html>
    <html>
        <head>
      	<title>Arkanoid with canvas</title>
    		<link rel="stylesheet" type="text/css" href="arkanoid.css">
    		<script type="text/javascript" src="arkanoid.js"></script>
    	</head>
    	<body onload="arkanoid.init();">
    	</body>
    </html>

Esto está claro: sólo tenemos un DOM HTML5, en donde asignamos un título, una referencia a un archivo CSS para que nos de los estilos a la página. Luego, por supuesto, la referencia a nuestro script, en donde se encontrará toda la lógica de la aplicación. Vamos a suponer por ahora que este archivo JavaScript expone un objeto llamado `arkanoid`, el cuál tiene un método llamado `.init()` al que podemos llamar. Eso lo hacemos, por supuesto, en el momento en que la página carga.

Ahora, los estilos no deben ser complejos tampoco. Todo lo que necesitamos es que en el cuerpo de la página exista un canvas y que este se vea como ocupando todo el espacio disponible. Por supuesto que esto significa poner los márgenes y los paddings a cero, pero lo que yo no sabía es que para evitar tener scrollbars o espaciados innecesarios, debemos indicar específicamente que el objeto canvas va a comportase como bloque, y que **todo** en la página carezca de espaciados. Esto lo aprendí de [una respuesta de StackOverflow](http://stackoverflow.com/questions/4288253/html5-canvas-100-width-height-of-viewport).

