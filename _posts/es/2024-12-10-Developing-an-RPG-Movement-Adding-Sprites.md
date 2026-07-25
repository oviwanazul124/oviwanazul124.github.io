---
title: Desarollando un RPG en Godot - Movimiento y añadiendo los sprites
date: 2024-12-14 12:00:10 +0100

categories: [Game Develop]
tags:
  - Godot
  - Game Develop
  - Tutorial
  - Maths
  - Spanish

excerpt: Esto es una serie de posts del blogs en que aprenderemos como desarrollar un juego RPG en Godot. En este blog nos centraremos en el movimiento y en añadir los sprites.

toc: true
toc_sticky: true
use_math: true

language: es
ref: developing-RPG-adding-sprites
lang_en: /en/developing-RPG-adding-sprites
lang_es: /es/developing-RPG-adding-sprites
lang_ja: /jp/developing-RPG-adding-sprites
permalink: /es/developing-RPG-adding-sprites

header:
  overlay_image: /assets/images/Develop-an-RPG-2/Header.gif
  overlay_filter: 0.25
---

## Movimiento

Una de las cosas más basicas es de los movimientos, es raro los juegos que no tienen algún tipo de movimiento pero existen. Actualmente voy a hablar del movimiento 2D en videojuegos.

### Matematicas y fisicas básicas del movimiento 2D

Primero de todo debemos enteder como funciona el movimiento en 2D. Y entonces podríamos añadir una tercera dimension. Pero por ahora eso será para un posts futuro. EL movimiento en videojuegos proviene de un vector, tampoco vamos a centrarnos muy a fondo sobre la matematica del vector.

$$\vec{B}=\begin{bmatrix}\vec{i} \vec{j}\end{bmatrix}$$

![Vector-Base](/assets/images/Develop-an-RPG-2/Vector-Base.png)

**i** es lo mismo que si dijera **x**, **j** es lo mismo que dijera **y**.
{: .notice--info}

La gran mayoría del movimiento viene cuando dicho vector cambia, por ejemplo, si definimos un vector llamado **u**.

$$\vec{u}=\begin{bmatrix}  0, 0\end{bmatrix}$$

Este vector define que nuestro personaje se encuentra en la posición x = 0, y = 0. Pero si por ejemplo nuestro personaje se moviera 2 veces hacía arriba, el vector cambiaría.

$$\vec{u}=\begin{bmatrix}  0, 2 \end{bmatrix}$$

![Vector-Example](/assets/images/Develop-an-RPG-2/Vector-Example.png)

Si observas el vector u esta formado por dos veces el vector j.

$$\vec{u}=\begin{bmatrix}  2\vec{i}, 0\end{bmatrix}$$

Esto es lo más básico para poder entender el movimiento de los videojuegos en 2D. En el futuro habrá un posts del blog más a fondo sobre esto.

## Movimiento en Godot

### Breve explicación

Los RPGs más clasicos o comunes utilizan el movimiento en 8, este movimiento permite al jugador moverse en todas las direcciones que quiera, usando **W**, **A**, **S**, **D**.

Para empzar vamos a crear una nueva carpeta en la raíz de nuestro proyecto, y la llamaremos **Scripts**. Aquí es donde vamos a guardar todo el código de nuestro juego.

![Godot-Explorer-Created-Scripts](/assets/images/Develop-an-RPG-2/Created-Folder-Scripts.png)

Despues de crear la carpeta de los script vamos a presionar click izquierdo y crear un script.

### Código

El código que vamos a escribir es el siguiente.

```gdscript
extends CharacterBody2D
```

Ahora vamos a compreder esta linea de código, **extends CharacterBody2D**, extends se encargá de importar todas las funciones asociadas a [CharacterBody2D](https://docs.godotengine.org/en/stable/classes/class_characterbody2d.html). Solo puede existir un extends por Script, y estará asociado al objeto al que hemos puesto el script.

Si quieres saber más sobre el CharacterBody2D haz click en su nombre y serás redireccionado a la documentación oficial de Godot.
{: .notice--info}

#### Variables

```gdscript

extends CharacterBody2D

@export var walking_speed = 400
@export var running_speed = 800
```

Ahora hemos añadido dos nuevas lineas de códgio, así es como defines una variable en Godot **var [nombre de la variable] = [valor]**, pero ¿Qué es @export?, cuando veas una palabra y antes de ella una "@" se usa para indicar que en este caso exporte dicha variable a la interfaz del motor , par aasí poder modificarlo sin necesidad de abrir el script.

#### Funciones

Ahora, vamos a definir dos funciones principales de este script la primera es **get_input()**, como su nombre indica de esta función es donde obtendremos el input del jugador, y la otra será **\_physics_process(delta)**, esta función viene por defecto en godot, y se encarga de actualizar y correr el código de fisicas en cada frame.

La variable delta es usada para calcular la actualización de frame, es una variable muy interesante y será investigada en un blog más a fondo.
{: .notice--info}

```gdscript

extends CharacterBody2D

@export var walking_speed = 400
@export var running_speed = 800

func get_input():
  pass

func _physics_process(delta):
  pass
```

#### Función get_input()

Ahora vamos a centrarnos en la función **get_input()**. Esta función se encarga de que el vector dirección de las teclas de input, **izquierda**, **derecha**, **arriba**, **abajo**. ¿Pero para que sirven estas teclas?, en un momento lo vamos a ver, pero ahora vamos a centrarnos en el if que hay aquí, este se encargá de verificar si el jugador quiere correr o andar, si pulsas la tecla **shift** el código usará la variable **running_speed** y si no utilizará **walking_speed**

```gdscript
func get_input():
  var input_direction = Input.get_vector("left", "right", "up", "down")
  if Input.is_action_just_pressed("shift"):
    velocity = input_direction * running_speed
  else:
    velocity = input_direction * walking_speed
```

#### Configurando los inputs

Para abrir el mapa de inputs (donde configuraremos los inputs), deberemos primero pulsar arriba a la izquierda donde pone **proyecto**, luego **configuración de proyecto** y por último **mapa de entrada**.

![Godot_Input_Map](/assets/images/Develop-an-RPG-2/Godot-Input-Map-Window.png)

Tras esto vamos a escribir donde pone **añadir una nueva acción**, **left**, y presionar **añadir**, y cuando presionemos veremos que cambia a algo similar a esto.

![Godot_Input_Map_Added_Input](/assets/images/Develop-an-RPG-2/Godot-Iput-Map-Added-Input.png)

Lo siguiente que vamos a hacer es presionar el **signo +**, y presionar la tecla que queremos vincular a ese input, y posteriormente pulsamos **aceptar**.

![Godot_Input_Map_Added_Input_Key](/assets/images/Develop-an-RPG-2/Godot-Input-Map-Added-Input-Key.png)

Ahora repetremos el mismo proceso para la tecla **right**, **up** y **down**.

#### Función \_physics_process(delta)

Ahora nos centraremos en ver **\_physics_process(delta)**, esta función es proporcionada por el engine y se encarga de todos los procesos relacionados con la fisicas del motor, aquí llamaremos a nuestra función **get_input()** y la función **move_and_slide()**, esto es también una función creada por el motor que dice al objeto que aplique fisicas.

```gdscript
  func _physics_process(delta):
    get_input()
    move_and_slide()
```

Si tienes un aviso en **delta** pon un \_ así **\_delta**
{: .notice--warning}

## Añadiendo un script y creando el jugador

Lo siguiente que vamos a hacer es presionar click izquierdo en **Node2D** y presionar **Añadir hijo**, se abrirá una ventana donde tendremos que buscar **CharacterBody2D** y añadirlo.

![Adding_CharacterBody2D](/assets/images/Develop-an-RPG-2/Adding-CharacterBody2D.gif.gif)

Si notienes un **Node2D** en la escena, añadelo de la misma forma que el CharacterBody2D.
{: .notice--warning}

Vas a ver un aviso a lado del nombre, ahora mismo no le vamos adar importancía. Tras esto, pulsaremos de nuevo el click izquierdo pero esta vez en **CharacterBody2D** y añadiremos un **Sprite**.

![Adding_Sprite](assets/images/Develop-an-RPG-2/Adding-Sprite.gif)

Ahora solo queda una cosa y es añadir el script al CharacterBody2D.

![Adding_Script_To_CharacterBody2D](assets/images/Develop-an-RPG-2/Adding-Script-To-CharaterBody2D.gif)

## Github Demo

Aquí tienes acceso al [repo](https://github.com/oviwanazul124/How-to-make-an-RPG/tree/main/Developing%20an%20RPG%20in%20Godot%20-%20Movement%20and%20adding%20sprites) que contiene todos los archivos del RPG que estamos creando.
