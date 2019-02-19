---
layout: post
title:  "[Presentando] Imagen docker para servidor minecraft"
date: 2019-02-14 16:07:04 -0600
author: "@streameast"
categories: docker minecraft server servidor
comments: yes
---

En este post voy a mostrar una [imagen](https://github.com/streameast/docker-minecraft-server)
docker para levantar un servidor de minecraft de manera fácil y curiosa si eres
un entusiasta docker; si no sabes y tienes interés en la tecnología docker, tienes
mas información [aquí](https://www.youtube.com/watch?v=hQgvt-s-AHQ).

![docker](https://www.docker.com/sites/default/files/social/docker_facebook_share.png)

Desde hace algún tiempo eh tenido la armonía de jugar algo en cooperativo con los
amigos, montar un servidor, reunirnos un poco de pizza y darle a jugar, pero no nos
decidíamos que juego poner.

Después de pensarlo un poco llegamos a minecraft, un juego que ya todos hemos jugado,
pero normalmente solos y que definitivamente le añade un toque especial jugar con
otros y la ventaja de que es multiplataforma, ya que no todos tienen Windows en su PC.

Creo que vi alguna imagen ya existente para este mismo propósito, pero tenia unas
ganas por compilar mi propia imagen así que decidí hacerlo de esa manera.

## Construcción y uso

Por motivos de la licencia de minecraft no esta en docker-hub, por lo que se compila
manualmente, pero esto es relativamente sencillo.

```bash
git clone https://github.com/streameast/docker-minecraft-server.git
cd docker-minecraft-server
docker build -t streameast/minecraft-server .
docker run -d -p 25565:25565 streameast/minecraft-server
```

## Curiosidades

Durante la ejecución en el servidor donde finalmente esta el servidor me di cuenta
de algo, esta computadora tiene apenas 1GB de RAM y la memoria recomendada por Mojang
es igualmente de 1GB de RAM exclusiva para la aplicación, por lo que no había suficiente
para ejecutarlo.

Debido a esto se crearon las variables MINECRAFT_XMX y MINECRAFT_XMS que manejan la
memoria asignada a la aplicación, volví a ejecutar la imagen asignando 512M a las
dos variables y funciono muy bien, el consumo se mantiene por los 700MB.

Mas información en la pagina del [proyecto](https://github.com/streameast/docker-minecraft-server).
