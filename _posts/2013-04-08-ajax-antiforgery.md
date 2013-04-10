---
layout: post
category : Security
tags : [ajax, security, antiforgery, forms-authentication, mvc, CSRF, XSRF]
title: Antiforgery Token for AJAX
author: amoschini
image: /img/posts/2013-04-08-ajax-antiforgery.jpg
---

Como sabrán, utilizando _Forms Authentication_, si no tenemos especial cuidado es 
muy fácil exponer nuestra aplicación a _Cross-site Request Forgery Attacks_ o 
_CSRF_, Phil Haack lo explica muy claramente en su post [Anatomy of a Cross-site 
Request Forgery Attack](http://haacked.com/archive/2009/04/02/anatomy-of-csrf-attack.aspx).

Básicamente esto significa que un sitio malicioso podría realizar una petición 
a nuestro sitio y utilizando nuestra cookie de autenticación y así utilizar los 
permisos del usuario para realizar una acción indeseada por este.

Por ejemplo, supongamos que nuestro sitio es un banco y mediante una API REST 
exponemos un servicio `http://www.mybanco.com/account/transfer`. Nuestro usuario 
está logueado revisando sus cuentas y recibe por email un link de una página de 
_chicas lindas_. Él, sin dudarlo, ingresa a dicha página, desde donde 
se realiza un POST nuestro servicio `transfer` solicitando una transferencia desde 
la cuenta del usuario a una cuenta bancaria en las islas Caiman. La transferencia 
es realizada ya que nuestro servicio recibe el request con la autenticación del 
usuario.

La forma más común de prevenirlo en una aplicación ASP.NET MVC consiste en 
utilizar el atributo [ValidateAntiForgeryToken](http://msdn.microsoft.com/en-us/library/system.web.mvc.validateantiforgerytokenattribute.aspx) en conjunto con 
el helper [Html.AntiForgeryToken()](http://msdn.microsoft.com/en-us/library/system.web.mvc.htmlhelper.antiforgerytoken.aspx). 

Internamente ASP.NET genera un token que es almacenado en una cookie [HttpOnly](https://www.owasp.org/index.php/HttpOnly) y el helper renderiza un input hidden con el 
nombre `__RequestVerificationToken`  y con el valor correspondiente a un hash del 
token; ese valor se envía en el POST de un formulario y al recibirlo una _action_ 
marcada con el atributo `ValidateAntiForgeryToken`, verifica que se correspondan 
el valor almacenado en la cookie y el valor `__RequestVerificationToken`.

Pero esto no es tan simple en llamadas AJAX si se utiliza `json` como `contentType` 
ya que por defecto _ASP.NET_ espera un parámetro `__RequestVerificationToken` codificado como `www-form-urlencoded`.

## La solución

### Server side

Siguiendo [las recomendaciones de Phil Haack](http://haacked.com/archive/2011/10/10/preventing-csrf-with-ajax.aspx) y actualizándolas para _ASP.NET MVC 4_ preparé la clase 
`ValidateJsonAntiForgeryTokenAttribute` que puede utilizarse para decorar 
_controllers_ o _actions_ de manera de que se obtenga el parámetro `__RequestVerificationToken` de los _headers_ del request.

{% highlight c# %}

    [AttributeUsage(AttributeTargets.Method | AttributeTargets.Class, AllowMultiple = false, Inherited = true)]
    public class ValidateJsonAntiForgeryTokenAttribute : FilterAttribute, IAuthorizationFilter
    {
        private const string key = "__RequestVerificationToken";
        public void OnAuthorization(AuthorizationContext filterContext)
        {
            if (filterContext == null)
                throw new ArgumentNullException("filterContext");

            var request = filterContext.HttpContext.Request;

            if (request.HttpMethod == "GET")
                return;

            HttpCookie cookie = request.Cookies[key];
            var cookieToken = cookie == null || String.IsNullOrEmpty(cookie.Value) ? string.Empty : cookie.Value;
            var formToken = request.Headers[key] ?? string.Empty;

            AntiForgery.Validate(cookieToken, formToken);
        }
    }

{% endhighlight %}

Además, no lo chequearemos para los GET, ya que se supone que estas acciones son 
de solo lectura y no presentan un peligro en este sentido, de esta manera 
podemos decorar un _controller_ entero, sin preocuparnos por las _actions_ GET.

### Client side

Desde el lado del cliente, debemos incluir el hash del token en nuestro 
_layout_:

{% highlight html %}

    <!DOCTYPE html>
    <html>
    <head>
        <link rel="shortcut icon" href="@Url.Content("~/Content/Images/favicon.ico")" type="image/x-icon"/>
        <title>@ViewBag.Title</title>    
    </head>
    <body>
        @Html.AntiForgeryToken() <!-- Acá está lo importante! -->
        @RenderBody()
    </body>
    </html>

{% endhighlight %}

Y desde _Javascript_, al realizar las llamadas AJAX debemos asegurarnos de incluir 
el parámetro `__RequestVerificationToken` en el header.

{% highlight javascript %}

    $.ajax({
        url: 'http://www.mybanco.com/account/transfer',
        data: { destinationAccount: '1241524545', amount: 500 },
        contentType: 'application/json; charset=utf-8',
        dataType: 'json',
        headers: { __RequestVerificationToken: $('input[name="__RequestVerificationToken"]').val() }, // Acá está lo importante!
        type: 'POST'
    });

{% endhighlight %}

Eso es todo, de esta forma simple ya tenemos nuestros servicios para AJAX un 
poco más protegidos.

## Disclamer

Recuerden que el código presentado aquí está realizado con fines didácticos y que 
no está listo para _copypastear_ y poner en producción.