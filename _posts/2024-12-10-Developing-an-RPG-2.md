---
title: Developing an RPG in Godot - Movement and adding sprites
date: 2024-12-14 12:00:10 +0100
categories: [Game Develop]
tags: [Godot, Game Develop, Tutorial, Maths, English]
description: This is a series of blog posts about how to develop a RPG game in godot. In this blog we are covering the movement and adding sprites.
math: true
image:
  path: assets/photos/Develop-an-RPG-2/Header.gif
  alt: A knight moving
---

## Movement

One of the basic things in video games is movement, which are rare games that don't have any type of movement but exist. But now I am going to talk about movement in 2D games.

### Mathematics and Physics of the 2D Movement

First, we need to understand how movement works in 2D. Then, we could talk about a third dimension. But the third dimension will be shown in a future blog post. Movement in video games comes from a vector. Right now, I would not enter too deeply into the concept.

$$\vec{B}=\begin{bmatrix}
  \vec{i}, \vec{j}
\end{bmatrix}$$

![Vector-Base](assets/photos/Develop-an-RPG-2/Vector-Base.png)
_Example of the vector base_

>**i** is the same as if I say **x**, **j** is the same as if I say **y**.
{: .prompt-info}

Most of the movement comes when a vector changes, if we define a vector named for example **u** from movement.

$$\vec{u}=\begin{bmatrix}
  0, 0
\end{bmatrix}$$

This vector means that our character is in the position x = 0 and y = 0. But if for example, our character moves 2 times up, the vector will change.

$$\vec{u}=\begin{bmatrix}
  0, 2
\end{bmatrix}$$

![Vector-Example](assets/photos/Develop-an-RPG-2/Vector-Example.png)
_Example of the vector movement_

If you see the vector u is formed by two times the vector j

$$\vec{u}=\begin{bmatrix}
  2\vec{i}, 0
\end{bmatrix}$$

This is the basics you will need to know to understand movement in videogames. In the future there will be more in deep blog post.

## Movement in Godot

### Brief explanation

The classic RPG uses the 8-movement, this type of movement enables the player to move in all directions they want, using **W**, **A**, **S**, **D**.

First of all, we are going to create a new folder at the root of our project, the folder will have the name "Scripts". Here we are going to save all the scripts to use in our game.

![Godot-Explorer-Created-Scripts](assets/photos/Develop-an-RPG-2/Created-Folder-Scripts.png)
_Created Folder Scripts_

After creating the folder script we are going to press left click and create a script.

### Code

The code we are going to write is the following.

```gdscript
extends CharacterBody2D
```

Now we are going to understand this line of code, **extends CharacterBody2D**, extends is in charge of importing all the functions associated to [CharacterBody2D](https://docs.godotengine.org/en/stable/classes/class_characterbody2d.html)

> If you wanna know more about the CharacterBody2D click in his name and you will be redirected to the official documentation of Godot.
{: .prompt-info}

Now we have added two new lines of code, this is how you define variables in Godot you put **var [name of the variable] = [value]**, but what is the @export? When you see this type of word with an "@" is used to indicate to the engine something about the variable in this case to export it, this means that you will see this variable in the engine and be able to modify it from there without the necessity of going to the script.

#### Variables

```gdscript

extends CharacterBody2D

@export var walking_speed = 400
@export var running_speed = 800
```

#### Functions

Next, we are going to define de two main variables of this script the first one is **get_input()**, as his name shows this is where we are going to get the input from, and the other one is **_physics_process(delta)**, this is a function that comes with some nodes in godot, is in charge of updating the physics every frame.

> The variable delta is used when you update something every frame, is a really interesting variable and there will be a deeper in a future blog post.
{: .prompt-info}

```gdscript

extends CharacterBody2D

@export var walking_speed = 400
@export var running_speed = 800

func get_input():
  pass

func _physics_process(delta):
  pass
```

#### Function get_input()

Now we are going to center in the function **get_input()**. This function is in charge to get the vector of direction of the input keys, **left**, **right**, **up**, **down**. But what are these input keys?. In a moment we are going to see it, for now we are going to talk about the if statement that we see here, this is in charge of seeing if the player want to run or to walk, if the key **shift** is pressed the code is going to use the **running_speed** but if it not being pressed is going to use the **walking_speed**

```gdscript
func get_input():
  var input_direction = Input.get_vector("left", "right", "up", "down")
  if Input.is_action_just_pressed("shift"):
    velocity = input_direction * running_speed
  else:
    velocity = input_direction * walking_speed
```

#### Setting up input commands

To open the input map we are going to need to press the following buttons, first in the upper right press **proyect**, **configuration proyect** and the **input map**.

![Godot_Input_Map](assets/photos/Develop-an-RPG-2/Godot-Input-Map-Window.png)
_Godot Input Map Window_

After doing this you are going to write where it says **"Add new action"**, **left**, press the **add**, when pressing this you are going to see the following changes.

![Godot_Input_Map_Added_Input](assets/photos/Develop-an-RPG-2/Godot-Iput-Map-Added-Input.png)
_Godot Input Map Added Input_

Next you are going to press the **plus sign**, and press the key that you want to bind to that input. After press **accept**.

![Godot_Input_Map_Added_Input_Key](assets/photos/Develop-an-RPG-2/Godot-Input-Map-Added-Input-Key.png)
_Godot Input Map Added Input Key_

We are going to follow the same procces with, **right**, **up** and **down**.

#### Function _physics_process(delta)

Next we are going to view the **_physics_process(delta)** this function is created by the engine and is in charge of all the process related to the physics, here we call our **get_input()** function, and the **move_and_slide()** functions, this is also a function created by the engine, and tell the object to start moving.

```gdscript
  func _physics_process(delta):
    get_input()
    move_and_slide()
```

> If you get a warning in **delta** add an underscore like this **_delta**
{: .prompt-warning}


## Adding the script and creating the player

Next we are going to press left click in **Node2D** and press **Add Child Node**, it is going to open a windows, there search **CharacterBody2D** and add it.

![Adding_CharacterBody2D](assets/photos/Develop-an-RPG-2/Adding-CharacterBody2D.gif.gif)
_Adding Character Body2D_

> If you don't have a **Node2D** in the tree, added in the same form as the characterBody2D.
{: .prompt-warning}

You are going to see a warning next to the name, you don't need to give importance to that right now. After that, do the same this time left clicking in the **CharacterBody2D**, and adding a **Sprite**.

![Adding_Sprite](assets/photos/Develop-an-RPG-2/Adding-Sprite.gif)
_Adding Sprite_

Now there is only one more thing left, adding the script to the CharacterBody2D.

![Adding_Script_To_CharacterBody2D](assets/photos/Develop-an-RPG-2/Adding-Script-To-CharaterBody2D.gif)
_Adding Script To CharacterBody2D_

## Github Demo

Here you can access to the [repo](https://github.com/oviwanazul124/How-to-make-an-RPG/tree/main/Developing%20an%20RPG%20in%20Godot%20-%20Movement%20and%20adding%20sprites) that contains all the files of the different blogs about developing and RPG.
