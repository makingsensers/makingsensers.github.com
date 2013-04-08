---
layout: post
category : Security
tags : [ajax, security, antiforgery, forms-authentication, mvc, CSRF, XSRF]
title: Antiforgery Token for AJAX
author: amoschini
---

Como sabrán, utilizando Forms Authentication, si no tenemos especial cuidado es 
muy fácil exponer nuestra aplicación a _Cross-site Request Forgery Attacks_ o 
_CSRF_, Phil Haack lo explica muy claramente en su post [Anatomy of a Cross-site 
Request Forgery Attack](http://haacked.com/archive/2009/04/02/anatomy-of-csrf-attack.aspx).

La forma más común de prevenirlo en una aplicación ASP.NET MVC consiste en 
utilizar el atributo [`ValidateAntiForgeryToken`](http://msdn.microsoft.com/en-us/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) en conjunto con el helper [`Html.AntiForgeryToken()`](http://msdn.microsoft.com/en-us/library/system.web.mvc.htmlhelper.antiforgerytoken(v=vs.108).aspx). 

Internamente ASP.NET genera un token que es almacenado en una cookie [HttpOnly](https://www.owasp.org/index.php/HttpOnly) y el helper renderiza un input hidden con el nombre `__RequestVerificationToken`  y con el valor correspondiente a un hash del token; ese valor se envía en el POST de un formulario y al recibirlo una _action_ marcada con el atributo `ValidateAntiForgeryToken`, verifica que se correspondan el valor almacenado en la cookie y el valor `__RequestVerificationToken`.


). Pero esto no es tan simple en llamadas AJAX.

....
http://haacked.com/archive/2011/10/10/preventing-csrf-with-ajax.aspx