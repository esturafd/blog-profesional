---
layout: post
title:  "[Presentando] HTTPS en GitHub Pages"
date: 2019-01-04 21:13:19 -0600
author: "@streameast"
categories: https ssl github-pages free
comments: yes
---

En este tiempo que tu sitio en internet tenga compatibilidad con https es muy
necesario, pero para los estudiantes o para los que no tienen experiencia se pueden
preguntar que opciones hay y si hay alguna gratuita.

Por defecto si tienes un dominio `*.github.io`, este ya tiene compatibilidad con
https, y si quieres que se use por defecto hay un configuración en la pestaña
settings de tu repositorio. Pero para los dominios personalizados es otra historia.

Si estas interesado en configurar tu dominio personalizado para GitHub Pages pero
no sabes como, te dejo el [link](https://help.github.com/articles/quick-start-setting-up-a-custom-domain/)
a la ayuda de GitHub.

## Cloudflare

Es un empresa que proporciona una red de entrega de contenido, servicios de seguridad
de Internet y servicios de servidores de nombres de dominio distribuidos, localizados
entre el visitante.

En un principio estaba confundido creía que Cloudflare era un gestor de dominios
por lo que creí que necesitaba que comprar otro dominio o algo, pero esta empresa
lo que ofrece es un servicio de DNS ademas de una realizar una funciona de proxy y
protegerte de por ejemplo ataques de DDoS, entre otras cosas.

Pero el servicio de DNS ya lo realiza el gestor de dominios, eso no importa por que
normalmente te deja configurar uno personalizado, un servername que proporciona
este servicio.

## Configuracion en Cloudflare

* Primero necesitamos registrarnos en la pagina de Cloudflare. Para esto hay un
menu para colocar nuestro correo electrónico y una contraseña.

![https://ibb.co/q9yYwMd](https://i.ibb.co/DkVfnDt/image.png)

* luego registramos el dominio, en la esquina superior derecha aparece "Add site",
y agregamos nuestro dominio.

![https://ibb.co/Tcq4nJH](https://i.ibb.co/R243MtC/image.png)
* Al realizar esto importara nuestra configuración de DNS actual, nos pondrá un
menú por si queremos cambiar una configuración, si no es el caso, continuamos.

* Hasta este punto aun no sabe si el dominio es nuestro, pero esto es facil, solo
falta cambiar los servername del servicio de DNS en nuestro gestor de dominio. En
mi caso es NameCheap pero deberia servir para cualquiera.

![https://ibb.co/Qft9TN1](https://i.ibb.co/jTshQM1/image.png)

* En Cloudflare, en la opción Crypto se coloca Full, esto hará que el certificado
se cree (esto puede tarda un tiempo).

![https://ibb.co/jk8RYSB](https://i.ibb.co/3mTzbnG/image.png)

Listo ya esta configurado, adicional podemos agregar una regla de pagina para
obligar a usar solamente https. Esto lo hacemos en la opcion "Page Rules", "create
Page Rule", colocamos `http://*midomin.io/*` (el primer asterisco para que aplique
a todos los subdominios y el segudo a todas las paginas de ese dominio) y añadimos
la configuración (Add a Setting) "Always Use HTTPS".

Revisa las referencias a recursos en tu pagina, el cambio puede dar algunos problemas.
En mi caso tenia algunas referencia absolutas, pero al cambiarlas a relativas y se
solucionaron.

¿Cual es tu excusa para con colocar https a tu sitio?
