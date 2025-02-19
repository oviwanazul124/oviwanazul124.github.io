---
title: Developing an RPG in Godot - Making the first objects
date: 2025-01-06 12:00:10 +0100
categories: [Game Develop]
tags: [Game Develop, Maths, English]
description: In this third blog post we are gonna develop the first objects, learning also about a really easy method to implement new things to our game.
math: true
image:
  path:
  alt: Developing-an-RPG-3
---

## What we refers as an object?

---

When I talk about an object, I refer to **everything that a player can interact**, for example in various RPG, you interact with **objects on the floor**, **people**...

Then everything that is interacteable is an object, obviously an person and a object in the floor **has differents workflows**, and **object** in the floor **only exist to be taken by the player**, but the person **maybe give you a mission** or it is a **shop** where it can be bought certain items. 

Now here enters the problem if an object can do all the things I have talked and more. The script that makes him work it would be **huge**, no?. Thats what I am gonna to talk next, in my opinion to make a game development much easier, this type of thinking would be obvious if you come from other area of computer development, but people that start in this world may not seen it as easy as others, so the next point is not needed to be readed for the guide.

## The type of thinking

---

When we start to develop our first scripts, it is recommended that we separate the main functions. Why is this?


It is a simple way to facilitate later the modification and understanding of this code in the future, in a simple way if in the future you have to modify a code that refers to 500 different nodes it will be much more complex to fix minimal errors than one that refers to 3 or 4 nodes. My recommendation is to always reduce the code to the minimum. Neither overthink it nor minimize it to the maximum, I know it sounds difficult but it is a skill that you get with time.

## Making our first object

---

### Creating the sample object

---

Now, we are gonning to make an object, the **first thing** we need to do is **make a new scene**. Why this?, making a new scene will allow us later to append that scene to others scene, this will be easier than remaking the object every moment that we need.

![Creating-Scene-First-Object]()
_Creating the scene for the first object_

>It would be recommended that in the root folder of the project you make a folder to save all the objects that you made also name the scene something obvious about what is inside, something you will remember even in months.
{: .prompt-info}

Now in the scene we will select the **[Node2D](https://docs.godotengine.org/en/latest/classes/class_node2d.html)** as a base, and add the following nodes as his childrens first we add an **[RigidBody2D](https://docs.godotengine.org/en/latest/classes/class_rigidbody2d.html)** after that we add inside of the RigidBody2D an **[Sprite2D](https://docs.godotengine.org/en/latest/classes/class_sprite2d.html)** and a **[CollisionShape2D](https://docs.godotengine.org/en/latest/classes/class_collisionshape2d.html)**, then a **[Area2D](https://docs.godotengine.org/en/latest/classes/class_area2d.html)** inside of the **[Area2D](https://docs.godotengine.org/en/latest/classes/class_area2d.html)** we are going to add another **[CollisionShape2D](https://docs.godotengine.org/en/latest/classes/class_collisionshape2d.html)**

![Root-of-the-object](assets/photos/Develop-an-RPG-3/Root-of-the-object.png)
_Heriarchy of the object_

> Why a **RigidBody2D** and not a **Body2D**?. As his name shows a RigidBody2D is for the objects that is only meant to be static, the first object that we are gonna to add to the game is going to be statics, in later blogs posts we are going to explore more this topic.
{: .prompt-info}


### Explanation of every node

---

The Node2D is the basics of every 2D node as his name indicates, will be used in all games made in 2D in this engine, now the RigidBody2D is a type of Body2D as seen above the main difference is that **Body2D** is mainly used for objects meant to move for example an enemy, an NPC or even our protagonist. In the other hand the RigidBody2D is meant for objects that are static, this type of body can move but the mainly use for, is for statics objects. There is also an **StaticBody2D**, this type of Body2D will appear in much later blogs posts.

### The code 

---

Now we are going to enter in the code section, we will be using a really basic script right now to dialog. For now we will start creating the script in the **InteracteableObject** or the **Node2D**. We are going to name it: **objectController**

> You can name it whatever you want, I am using this to maintain certain order with my scripts
{: .prompt-info}

Next we are going to delete the ***_process()*** and ***_start()*** function, this two function is not going to be used right now in the script. Next we are going to create the first custom functions we are going to call it ***_on_body_entered()***, this function will be in charge of detecting when the Player is interacting with the radius of interaction. The script should look like the following:

```gdscript

extends Node2D


_on_body_entered():
  pass

```

After creating the function we are going to define a variable named **isInside** this will be a bool, that will be in charge of checking if the player is inside the radious of interaction

> Always name your variables something that is meaningful to that variable. If you call it for example **"j"** soon or later you are going to forget what even that name is about.
{: .prompt-warning}

```gdscript

extends Node2D

var isInside : Bool = false

_on_body_entered():
  isInside = true

```

If you see this time we defined the variable in a different form, normally we use **var isInside = false**, but in this case we use **var isInside *: Bool* = false**, in this case the ***: Bool*** part is used to mark that **ONLY A BOOL VALUE** can be save in that variable and cannnot be asigned other one.

> This type of definitions follow the following syntax: **var *[Name of the variable]* : *[Type of variable]* *(Optional [Definition of the variable])***
{: .prompt-info}

Next we are going to create a function to check when the player has exited the radious of interaction of the object. We are going to call it ***_on_body_exited()***.

```gdscript

extends Node2D

var isInside : Bool = false

# This function check if the player is inside of the interaction radious
_on_body_entered():
  isInside = true

# This function check if the player is outside of the interaction radious
_on_body_exited():
  isInside = false

```
Now we are going to use a function called ***_input()*** this is a engige function that is called every time that an input event is made. For example if a key is pressed, we are going to use this function to check if our interaction button has been pressed and the player is inside of the interaction radious of the object.

```gdscript

extends Node2D

var isInside : Bool = false

# This function check if the player is inside of the interaction radious
_on_body_entered():
  isInside = true

# This function check if the player is outside of the interaction radious
_on_body_exited():
  isInside = false

_

```
