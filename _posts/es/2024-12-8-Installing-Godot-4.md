---
title: Instalando Godot 4
date: 2024-12-8 12:00:10 +0100

categories: [Game Develop]
tags:
  - Godot
  - Game Develop
  - Tutorial
  - Spanish

toc: true
toc_sticky: true
excerpt: Esto es un tutorial sencillo para instalar Godot 4

language: es
ref: installing-godot-4
lang_en: /en/installing-godot-4
lang_es: /es/installing-godot-4
lang_ja: /jp/installing-godot-4
permalink: /es/installing-godot-4

header:
  teaser: /assets/images/Develop-an-RPG/GodotMainPage.png
  overlay_image: /assets/images/Develop-an-RPG/GodotMainPage.png
  overlay_filter: 0.25
---

## Introducción

En esta serie de posts del blog, vamos a aprender a como desarrollar un RPG en Godot. Existen múltiples engines que podemos usar para crear un videojuego, como pueden ser **Unity**, **Unreal Engine** pero vamos a elegir **Godot** por las razones personales a continuación.

## ¿Porqué Godot?

Godot es un **motor de código abierto que es de uso gratuito**. Puedes donar para su desarrollo, pero si comienzas como un hobby en el desarrollo de videojuegos pienso que es una de las mejores opciones en el momento.

No todo es perfecto, siempre hay algunas **pegas**, por ejemplo a la hora de escribir esto, la comunidad esta todavía en auge así que tendrás **más dificultad de encontrar tutoriales en tu idioma natal** y tendrás que usar la **documentación**. Junto a esto Godot usa su propio lenguaje **GDScript** (Se puede usar C#, aunque se recomienda aprenderlo para obtener todo el potencial), que comparte similitudes con Python, Ruby y otros lenguajes cercanos a él.

## Instalando el motor

### Desde la página web

Para instalarlo existen dos formas, la primera es hacerlo desde la web oficial, para ello tendrás que entrar en la web y pulsar el botón de descarga, y ejecutar el programa, para así tener instalado el motor.

![Godot-Main-Page](/assets/images/Develop-an-RPG/GodotMainPage.png){: .full}

### Páginas On-line

La segunda forma es descargar el motor desde páginas como itch.io o steam, para ello tendrás que ir a la página que prefieras y buscarlo.

![Godot-Steam-Page](/assets/images/Develop-an-RPG/GodotSteamPage.png){: .full}

Al menos en Steam el soporte para C# no esta incluido a sí que si decides usar C# deberás usar el metodo de la página web.
{: .notice--warning }

## Creando un nuevo proyecto

Cuando abres el engine verás algo similar a la foto de abajo, lo primero que tenemos que hacer es presionar el botón que esta marcado en rojo.

![Godot-Projects-Open](/assets/images/Develop-an-RPG/GodotProjectsOpen.png){: .full}

Cuando presiones el botón se te mostrará algo parecido a esto.

![Godot-Projects-Create](/assets/images/Develop-an-RPG/GodotProjectsCreate.png){: .full}

Aquí tendremos que introducir **el nombre del proyecto** y **donde será guardado el proyecto**. Además también tendremos una selección del modo de renderizado (gráficos) del proyecto, por ahora seleccionaremos **Forward+** (orientado a PC) y pulsaremos en **crear y editar**.

![Godot-Engine-Open](/assets/images/Develop-an-RPG/GodotEngineOpen.png){: .full}

Y con eso ya hemos instalado correctamente Godot Engine, en el próximo tutorial vamos a ver como añadir sprites y seleccionar el tipo del movimiento al personaje
