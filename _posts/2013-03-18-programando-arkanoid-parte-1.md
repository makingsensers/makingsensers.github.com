---
layout: post
image: /img/posts/2013-01-21-my-menu-invitacion.jpg
category : 
tags : 
title: Programando Arkanoid - Parte 1
author: jraimondi
---

****** TODO insert image http://blog.alphasmanifesto.com/wp-content/uploads/2013/03/arkanoid.jpg ******

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

Para esto podemos usar muy apropiadamente el selector de CSS *, que matcheará absolutamente todo elemento. Este selector se llama [Universal Selector](http://www.w3.org/TR/selectors/#universal-selector) y está disponble para los navegadores que soporten características de CSS3. Por supuesto, estamos trabajando en Canvas con lo que es muy factible que los navegadores que soportan el segundo también soporten el primero.

Nuestro CSS se ve, entonces, así:

	/* from http://stackoverflow.com/questions/4288253/html5-canvas-100-width-height-of-viewport */
	 
	* {
	    margin: 0;
		padding: 0;
	}
	 
	html, body {
		width: 100%;
		height: 100%;
	}
	 
	canvas {
		display: block;
	}

## El código

Para proceder a la parte de JavaScript, ya teníamos una limitación particular: debemos crear un objeto `arkanoid` que tenga la función `init()`. De una forma simplista entonces instanciaremos el objeto arkanoid asignándole un valor al objeto window, o podríamos haberla declarado de forma independiente. Para mayor seguridad, podemos devolver los resultados de una función auto-ejecutable, de forma que todas las variables que creemos sean locales y no estén manchando el namespace global.

Como también estaremos codificando lógica interna, seguramente querremos tener varias funciones y variables privadas. Nuestra función autoejecutable tiene solo que devolver entonces aquello que queramos hacer público, en nuestro caso, la función `init()`.

	window.arkanoid = (function(userOptions) {
	 
	  // private fields
	  var canvas = null;
	  var ctx = null;
	  var options = null;
	 
	  var defaultOptions = {
	    fullWidth: true,
	    fullHeight: true,
	    stageHeight: 600,
	    stageWidth: 1024
	  };
	 
	 
	  // private methods
	  function initOptions(userOptions) {
	    options = mergeObjects(defaultOptions, userOptions);
	    if (options.fullWidth) options.stageWidth = document.documentElement.clientWidth;
	    if (options.fullHeight) options.stageHeight = document.documentElement.clientHeight;
	  }
	 
	  function mergeObjects(toOverride, overridingWith) {
	    for (var property in overridingWith) {
	      toOverride[property] = overridingWith[property];
	    }
	    return toOverride;
	  }
	 
	  function initCanvas() {
	    var body = document.getElementsByTagName("body")[0];
	    var height = options.stageWidth;
	    var width = options.stageHeight;
	    canvas = document.createElement("canvas");
	    canvas.width = height;
	    canvas.height = width;
	    body.appendChild(canvas);
	    ctx = canvas.getContext("2d");
	  }
	 
	  function initAll() {
	    initOptions();
	    initCanvas();
	 
	    var stage = new ArkanoidStage(ctx, options.stageHeight, options.stageWidth);
	  }
	 
	  // public methods
	  return {
	    init: initAll
	  };
	})()

Vayamos analizando ese código línea a línea:

- **La línea 1 define el objeto `arkanoid` que necesitábamos.** Lo define como el resultado de una función que será llamada, y tiene la capacidad de recibir parámetros que serán las opciones del usuario. Esto es, en caso en que quisiéramos pasar información al momento de inicializarlo.
- **Las líneas 4 a 6 definen variables locales**, solamente disponibles para este objeto arkanoid, que serán utilizadas por las demás funciones interiores. Estas no estarán disponibles a los objetos externos al momento de devolver el resultado, y más aún, tampoco se encontrarán disponible a elementos que hagan referencias a `this` o a `self`. Si eso los confunde, a mí también me ocurrió, checkeen esta pregunta en StackOverflow: [JavaScript local scoping: var vs. this](http://stackoverflow.com/q/15046910/147507).
- **Las líneas 8 a 13 definen otra variable local**, pero esta será un objeto literal, para agrupar las posibles opciones con valores por defecto que tomaremos en caso en que el usuario (quien llama a esta función) no las provea.
- **Las líneas 17 a 21 definen la función `initOptions`**, que se encargará de identificar el conjunto de opciones válidas a utilizar, basado tanto en lo provisto por el usuario, los defaults, y la lógica interna. En este caso, obtendremos el override de lo que proveyó el usuario sobre lo default, y verificaremos que si estamos trabajando a pantalla completa (`fullWidth` y `fullHeight`), actualizaremos las variables de ancho y alto para que sean consistentes (`stageWidth` y `stageHeight`).
- **Las líneas 23 a 28 hacen la magia de obtener el conjunto de opciones desde los defaults y con lo que el usuario proveyó.** La lógica es tan simple como copiar todo lo que el usuario nos dio sobre el objeto de las opciones por default. Cabe destacar que aquí estamos escribiendo sobre el objeto de destino, por lo que si quisiéramos volver al valor por defecto, ya lo habríamos perdido. Una forma simple de haber hecho esto es, en lugar de llamarlo así:

	    options = mergeObjects(defaultOptions, userOptions);

Deberíamos llamarlo así:

    options = mergeObjects({}, defaultOptions); // creates a copy
    options = mergeObjects(options, userOptions); // overrides defaults

- **Las líneas 30 a 39 inicializan el objeto canvas que se utilizará.** Muy básicamente se obtiene el objeto body, se crea un objeto `canvas` y se le anexa, con el tamaño apropiado según las opciones. Para uso posterior, se almacenan las referencias al canvas y al contexto de dibujo 2D.
- **Las líneas 41 a 46 realizan ese trabajo en sucesión** llamando a las funciones apropiadas, e inicializa el stage sobre el que la magia ocurrirá.
- Por último, **las líneas 49 a 51 devuelven el objeto** exponiendo sólo la última función, y dándole el nombre de `init`.

Por ahora nos detendremos aquí y continuaremos en la parte dos. Mientras lo preparo, estoy dispuesto a responder preguntas, y seguramente las preguntas y los comentarios ayudarán a generar las partes posteriores.
