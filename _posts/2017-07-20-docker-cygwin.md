---
layout: post
title:  "[Instalación] Docker Toolbox en Cygwin"
date:   2017-07-20 14:23:44 -0600
author: "@streameast"
categories: docker cygwin wimpty
comments: yes
---

Bueno, es el segundo post, no es mi intención solo hablar solo de Cygwin pero 
es una de las herramientas que más uso, también estoy consciente que Windows
ya tiene una solución propia y puede ejecutar bash, pero tengo que formatear mi
PC y después de eso lo probare, mientras tanto sigamos.

## ¿ Que es Docker ?
Docker es una plataforma de contenedores para aplicaciones, que empaqueta
una aplicación y sus requisitos para que la ejecución no dependa de las 
configuraciones del ambiente si no solo del contenedor, además de varias
otras funcionalidades, para más información 
[aquí](https://www.docker.com/what-docker).

## ¿ Que es Cygwin ?
Cygwin es una larga colección de herramientas GNU y Open Source, las cuales
proveen una funcionalidad similar a una distribución Linux en Windows, para 
más información [aquí](https://www.cygwin.com).

## ¿ Por que Cygwin ?
Docker ya viene con una herramienta similar a Cygwin para ejecutarlo, pero 
dado que yo ya tenía Cygwin, además de una serie de configuraciones 
personalizadas, la idea es poder seguir usando Cygwin.

## Instalación

Lo primero sería descargar 
[Docker Toolbox](https://download.docker.com/win/stable/DockerToolbox.exe), 
si buscas en la página oficial te aparecerá la versión CE, pero esta requiere
un Windows Profesional o Enterprise.

La instalación del propio Toolbox no es distinta a una instalación en 
Windows, más información [aqui](https://docs.docker.com/toolbox/toolbox_install_windows/#step-2-install-docker-toolbox).

Si ejecutas el comando docker antes de ejecutar Docker Quickstart Terminal, puedes ver que hay un problema

```
$ docker version
Client:
 Version:      17.05.0-ce
 API version:  1.29
 Go version:   go1.7.5
 Git commit:   89658be
 Built:        Fri May  5 15:36:11 2017
 OS/Arch:      windows/amd64
error during connect: Get http://%2F%2F.%2Fpipe%2Fdocker_engine/v1.29/version: 
open //./pipe/docker_engine: El sistema no puede encontrar el archivo especificado. 
In the default daemon configuration on Windows, the docker client must be run 
elevated to connect. This error may also indicate that the docker daemon is not running.

```

Cuando yo instale Docker, y al ejecutar Docker Quickstart Terminal me dio 
el primer error pero este se solucionó reiniciando el PC, la ejecución del
Quickstart es para crear la máquina virtual donde se crearan los contenedores
pero como la idea es usar Cygwin creémosla ahí, aunque se puede crear con
la herramienta que te da Docker.

el comando ``docker-machine`` sirve para administrar la máquina virtual, 
la cual por defecto se crea con el nombre "default", si la quisiéramos 
crear con ese nombre ejecutamos:

``docker-machine create default``

una ves creada se necesita que se creen las variables que docker usa para 
ejecutarse, las cuales se pueden crear ejecutando

``eval $(docker-machine env default)``

## Configuración

Una de las primeras cosas que podemos hacer es ejecutar ``docker version``
en cygwin, y ya se ejecutara correctamente, el problema es que si queremos
crear un contenedor o descargar una imagen de los repositorios oficiales
se va quedar ejecutando pero el comando no termina, este problema es 
ocasionado debido a que Mimtty la consola que ejecuta cygwin es de tipo
TTY y el comando docker pide una de tipo PTY, encontré un poco de 
documentación sobre este error pero en su mayoría recomendaba usar la 
herramienta oficial.

Finalmente encontré un programa llamado wimpty el cual debe solucionar el
problema, y un instalador convenientemente fácil "[babun-docker](https://github.com/tiangolo/babun-docker)", 
pero esta no me funciono, y me toco que compilar [wimpty](https://github.com/rprichard/winpty),
para eso descargamos el [zip](https://github.com/rprichard/winpty/archive/master.zip) y lo descomprimimos o lo clonamos por git

```
git clone https://github.com/rprichard/winpty.git
mv wimpty .wimpty
cd .wimpty
./configure
make
make install
```

finalmente añadimos el uso de wimpty en el archivo ``.bash_profile`` que 
está en ``$HOME`` y listo

```
# docker
eval $(docker-machine env default)
alias docker='winpty docker'
export PATH=${PATH}:${HOME}/.winpty
```

Espero que les ayude y nos vemos en el próximo post!
