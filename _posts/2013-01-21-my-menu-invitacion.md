---
layout: post
image: /img/posts/2013-01-21-my-menu-invitacion.jpg
category : Self-Training / My Menu
tags : [selftraining, typescript, javascript, commonjobs]
title: My Menu - Invitación
author: andresmoschini
---

Trabajamos en una empresa de soft, desarrollamos software y somos buenos haciendoló. Por eso, creo que es bueno que participemos en el desarrollo y mejoras de las aplicaciones que utilizamos día a día. Ese es el caso del sistema de selección de las comidas diarias: nosotros deberíamos arreglarlo, mejorarlo, optimizarlo y, llegado el caso, reemplazarlo completamente.

_My Menu_ (sistema que presenté en un [post anterior][]) fue creado con el objetivo principal de probar y conocer algunas tecnologías, sé que el código y diseño no es el mejor. Tampoco está en producción actualmente. 

Igualmente, creo que tiene algunas características interesantes y que puede ser una buena base para continuar juntos el desarrollo de una herramienta que utilizamos todos los días. Por eso me decidí a invitar a que visiten el código fuente y a que propongan cambios y mejoras.

_My Menu_ forma parte de _[CommonJobs][]_, un sistema de uso interno del área de recursos humanos de la empresa, y utiliza su base de datos y servidores. 

En el assembly [CommonJobs.Domain.MyMenu][] se describe el dominio; en [CommonJobs.Application.MyMenu][] se utiliza la infraestructura de _CommonJobs_ para persistencia, y tareas recurrentes; y el grueso del código está en el proyecto [CommonJobs.Mvc.UI][] donde están los _ViewModels_ y los _templates_ de las páginas:

* [my-menu.ts][]
* [my-menu-pages.ts][]
* [my-menu-admin-page.ts][]
* [my-menu-order-page.ts][]
* [CommonJobs.Mvc.UI.Areas.MyMenu][]

Espero en futuros posts ir más en detalle sobre los puntos o tecnologías interesantes. Mientras tanto, ¡espero pull requests en GitHub!

### Bonus Track

Dado que no encontré ningún _datepicker_ con las características deseadas y que se integrara correctamente con _TypeScript_, _Bootstrap_, _Knockout_ y _Moment.js_, preparé [moment-datepicker][] basado en bootstrap-datepicker de Stefan Petre. Es simple, fácil de usar y tiene su [paquete de nuget][moment-datepicker-nuget] listo para utilizar en Visual Studio.


[post anterior]: http://makingsensers.wordpress.com/2012/12/26/self-training-my-menu/
[CommonJobs]: http://commonjobs.makingsense.com/documentation
[CommonJobs.Mvc.UI]: https://github.com/CommonJobs/CommonJobs/tree/master/source/CommonJobs/CommonJobs.Mvc.UI
[my-menu.ts]: https://github.com/CommonJobs/CommonJobs/blob/master/source/CommonJobs/CommonJobs.Mvc.UI/Scripts/my-menu.ts
[my-menu-pages.ts]: https://github.com/CommonJobs/CommonJobs/blob/master/source/CommonJobs/CommonJobs.Mvc.UI/Scripts/my-menu-pages.ts
[my-menu-admin-page.ts]: https://github.com/CommonJobs/CommonJobs/blob/master/source/CommonJobs/CommonJobs.Mvc.UI/Scripts/my-menu-admin-page.ts
[my-menu-order-page.ts]: https://github.com/CommonJobs/CommonJobs/blob/master/source/CommonJobs/CommonJobs.Mvc.UI/Scripts/my-menu-order-page.ts
[CommonJobs.Mvc.UI.Areas.MyMenu]: https://github.com/CommonJobs/CommonJobs/tree/master/source/CommonJobs/CommonJobs.Mvc.UI/Areas/MyMenu
[CommonJobs.Domain.MyMenu]: https://github.com/CommonJobs/CommonJobs/tree/master/source/CommonJobs/CommonJobs.Domain.MyMenu
[CommonJobs.Application.MyMenu]: https://github.com/CommonJobs/CommonJobs/tree/master/source/CommonJobs/CommonJobs.Application.MyMenu
[moment-datepicker]: http://makingsense.github.com/moment-datepicker/
[moment-datepicker-nuget]: https://nuget.org/packages/MomentDatepicker