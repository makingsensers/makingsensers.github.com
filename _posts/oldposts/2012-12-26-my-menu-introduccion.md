---
layout: post
category: Self-Training / My Menu
tags: [bootstrap, javascript, knockout.js, moment.js, nuget, typescript]
title: My Menu - Introducción
author: andresmoschini
---

En el marco del self-training `CAP-42` estuve experimentando con varias tecnologías en las que quería profundizar. Próximamente espero realizar una serie de posts con mis impresiones sobre cada una y de la interacción entre ellas.

### Las tecnologías

* [KnockoutJS](http://knockoutjs.com/) - Librería de JavaScript para facilitar la creación de interfaces web ricas y dinámicas mediante el patrón de MVVM, bindings y observables.
* [TypeScript](http://typescript.codeplex.com/) - Súper conjunto de JavaScript que le añade tipado opcional, clases y módulos. Al compilarse genera código JavaScript limpio y basado en estándares.
* [Twitter Bootstrap](http://twitter.github.com/bootstrap) - Framework CSS para desarrollar aplicaciones web rápidamente, con un estilo consistente, simple y agradable. También incluye algunas utilidades extensiones JavaScript.
* [NuGet](http://nuget.org/) - Extensión de Visual Studio para instalar y actualizar librerías de terceros (en realidad lo que me interesaba a mi era la publicación de paquetes).
* [Moment.js](http://momentjs.com/) - Librería JavaScript para parseo, validación, manipulación, y formateo de fechas.

### El sistema

El objetivo, a la vez de aprender, era desarrollar un sistema para simplificar la gestión de los pedidos diarios de comida realizados en la empresa.

El sistema se empezó a construir sin apuro, con la idea de investigar, experimentar y probar lo aprendido en un entorno real. Entre tanto, dado que ocurrieron algunos inconvenientes con los pedidos, en tiempo récord JF implementó e implantó un sistema con similar objetivo, el cual está cumpliendo muy bien su cometido. Por lo tanto, es probable que mi sistema nunca salga a producción.

De cualquier manera, está disponible para ser probado en [AppHarbor](http://commonjobs.apphb.com/MyMenu/admin) y, para los empleados de la empresa, como parte del sistema de uso interno [CommonJobs](https://commonjobs.makingsense.com/mymenu).

#### El problema

Cada día, antes de las 10 de la mañana, los empleados pueden elegir la comida del día entre 3 opciones (_Normal_, _Light_, _Vegetariano_). Los platos correspondientes a cada opción son diferentes cada día durante 5 semanas (pasados los cuales los platos se repiten).

Originalmente, estábamos utilizando una planilla de Google Docs para marcar las preferencias de cada empleado en cada día de las 5 semanas. Pero dado que esa planilla era compartida, no se permitía acceso de edición a todos y era complicado realizar modificaciones. Por otro lado, solía ocurrir que por una situación particular un empleado cancelara el menú de un día, y pasadas las 5 semanas no recibiera su comida ya que alguien olvidó quitar la _“cancelación”_.

Otra característica que me interesaba incluir, era la posibilidad de seleccionar el lugar donde comer. No es tan común, pero a veces ocurre que, un empleado, un día en particular, por ejemplo por una reunión, no coma en la oficina de siempre sino en otra, por lo que sería bueno que la comida se le envíe allí.

#### UI del empleado

Cuando el empleado entra al sistema, ve una pantalla con su selección para el día actual.

![Selección del día](/img/posts/2012-12-26-my-menu-introduccion/employee1.jpg)

Si ya ha pasado la hora límite para cambiar el pedido, se le indica con una barra amarilla que el pedido ya se realizó. Si aún hay tiempo para modificarlo, se le indica con una barra verde.

![Aún se puede editar!](/img/posts/2012-12-26-my-menu-introduccion/employee2.jpg)

El empleado puede marcar sus preferencias (menú y lugar) para cada día de las 5 semanas. Las fechas que se observan a la derecha son solo referencias: La configuración del _Lunes de la semana 2_ será válida tanto para el _28 de Enero 2013_ como para el _4 de Marzo_.

![Menú semanal](/img/posts/2012-12-26-my-menu-introduccion/employee3.jpg)

Se puede modificar la elección para días particulares, sobrescribiendo la elección semanal. Por ejemplo, si el empleado sabe que el día _9 de Enero de 2013_ (dentro de dos meses o mañana) no estará presente, puede cancelarlo indicando la fecha. De la misma manera puede modificarse el menú o lugar para una fecha puntual.

![Días específicos](/img/posts/2012-12-26-my-menu-introduccion/employee4.jpg)

Por último, todos los empleados pueden ver el resumen y detalle completo del pedido, lo cual es muy útil si alguno de ellos no puede acceder al sistema o hay que resolver una discusión acerca de un plato faltante.

![Pedido completo del día](/img/posts/2012-12-26-my-menu-introduccion/employee5.jpg)

#### UI de administración

El administrador del menú, además de ver el pedido del día, antes de las 10 de la mañana, puede generarlo por anticipado; O bien, luego de las 10, puede volver a generar un pedido en base a la selección actual de cada empleado.

![Pedido completo del día](/img/posts/2012-12-26-my-menu-introduccion/admin1.jpg)

También puede editar las selecciones de cualquier empleado.

![Selección de del empleado](/img/posts/2012-12-26-my-menu-introduccion/admin2.jpg)

Definir los platos correspondientes a cada día del menú.

![Definición del menú](/img/posts/2012-12-26-my-menu-introduccion/admin3.jpg)

Y redefinir completamente el menú: modificar o agregar opciones y lugares, cambiar las fechas y la cantidad de semanas.

![Opciones del menú](/img/posts/2012-12-26-my-menu-introduccion/admin4.jpg)

