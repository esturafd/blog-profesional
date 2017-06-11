---
layout: post
title:  "[Instalación] Jekyll en Cygwin"
date:   2017-06-11 16:23:44 -0600
author: "Estuardo Ramos"
categories: jekyll cygwin
---

Desde hace un tiempo que quería empezar a escribir un blog, para documentar
algunas cosas que hago y talves compartir algunas soluciones que eh encontrado,
ya saben de esas que te quiebras la cabeza tratando de solucionar y cuando 
terminas no tienes idea de lo que hiciste, bueno problema solucionado.

### ¿Por qué Cygwin?

Ya llevo un tiempo queriendo ser linuxero, pero por una u otra razón no
eh podido hacer que este sea mi sistema operativo principal, en el trabajo
uso Windows, como muchos y mi computadora personal de una forma u otra
acaba descompuesta o con algún otro inconveniente, por lo que no eh podido
al pie de la letra ser linuxero. A pesar de esto decidí instalar lo mas 
cercano a esto en Windows, Cygwin, y esto sumado a que trabajo con servidores
linux, quiero pensar que en mi interior tengo algo de linuxero.

### ¿Que es Jekyll?

Jekyll es un simple generador de sitios estáticos. Es un motor de análisis 
sintetizado como una gema de ruby que se utiliza para construir sitios web
estáticos a partir de componentes dinámicos como plantillas, código Liquid,
Markdown, etc.

### Instalación

Me hubiera gustado documentar cada uno de los pasos que hice pero esto lo 
esto escribiendo ya un tiempo después, así que vamos con un resumen:

Lo primero es instalar las dependencias necesarias del repositorio de Cygwin,
en la cuales instale los paquetes:

* ruby
* ruby-bundler
* ruby-devel

![cygwin-intall-ruby](https://lh3.googleusercontent.com/ux-wN46FJjoY3uhYaRnBu0oTFB8wJI_DDUXIE6ymDEJK4jJhXtNf_DVJRrqjg8JMwXwOUC8xjhrz8G0=w1366-h658)

Comprobamos que este instalado:

```
$ ruby --version
ruby 2.3.3p222 (2016-11-21 revision 56859) [x86_64-cygwin]

$ gem --version
2.6.11

$ bundler --version
Bundler version 1.15.1
```

Luego de esto instalamos la ultima dependencia por medio del comando gem:

`$ gem install bigdecimal`

Instalamos Jekyll:

`$ gem install jekyll`

Después de esto me tope con el problema que no funcionaba el comando jekyll,
pero revisando la ruta donde realice la instalación note una carpeta bin, la
cual no estaba con anterioridad, aqui estaban los ejecutables de las gemas
instaladas, así que me puse a ver si estas ya estaban en la carpeta de 
binarios y los que no los moví.

```
$ cd bin
$ ls -l
total 13
-rwxr-xr-x 1 usuario usuario 484 jun. 10 21:51 bundle
-rwxr-xr-x 1 usuario usuario 485 jun. 10 21:51 bundler
-rwxr-xr-x 1 usuario usuario 482 jun. 10 22:40 jekyll
-rwxr-xr-x 1 usuario usuario 488 jun. 10 22:14 kramdown
-rwxr-xr-x 1 usuario usuario 482 jun. 10 22:14 listen
-rwxr-xr-x 1 usuario usuario 476 jun. 10 21:42 rake
-rwxr-xr-x 1 usuario usuario 476 jun. 10 21:42 rdoc
-rwxr-xr-x 1 usuario usuario 474 jun. 10 21:42 ri
-rwxr-xr-x 1 usuario usuario 481 jun. 10 22:14 rougify
-rwxr-xr-x 1 usuario usuario 491 jun. 10 22:14 safe_yaml
-rwxr-xr-x 1 usuario usuario 476 jun. 10 21:27 sass
-rwxr-xr-x 1 usuario usuario 484 jun. 10 21:27 sass-convert
-rwxr-xr-x 1 usuario usuario 476 jun. 10 21:27 scss

$ for x in $(ls --color=never); do which $x; done
```

Por lo que solo queda moverlos, y si deseas hacer un backup

```
cp -r bin/ Backups/bingem/
mv bin/jekyll /usr/bin/
```

Y estamos listo para una prueba:

```
jekyll new blog-asombroso
cd blog-asombroso
jekyll serv
```

![jekyll-serve](https://lh4.googleusercontent.com/I0fZO_poWEY7Ggujcm44eqt60S3ospmxK77X4cUJLUc-8-hH9ty151JByK2Mdk53J5zTcO-zLZq0LU4=w1366-h658-rw)

Nos vemos en el proximo post!
