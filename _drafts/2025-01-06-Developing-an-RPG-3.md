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

When I talk about an object, I refer to **everything that a player can interact**, for example in various RPG, you interact with **objects on the floor**, **people**...

Then everything that is interacteable is an object, obviously an person and a object in the floor **has differents workflows**, and **object** in the floor **only exist to be taken by the player**, but the person **maybe give you a mission** or it is a **shop** where it can be bought certain items. 

Now here enters the problem if an object can do all the things I have talked and more. The script that makes him work it would be **huge**, no?. Thats what I am gonna to talk next, in my opinion to make a game development much easier, this type of thinking would be obvious if you come from other area of computer development, but people that start in this world may not seen it as easy as others, so the next point is not needed to be readed for the guide.

## The type of thinking

> This section is a TIP, you dont need to take this as a manual, everyone has different workflows.
{: .prompt-warning}

To solve this problem, we are gonna to think in the real world, imagine you are in apartament and you are hungry, the most obvious thing that you would do it going to be to go to the kitchen and make something to eat, now in the context we are going to have two kitchens.

The **first kitchen**, have everything in a right place, every cabinet store a type of thing and not various for example, one is only for the drinks, vegetables... In this kitchen will be easier to find what you need in no matter of time and also it would be easier to others.

![First-kitchen-example]()
_Example of the first kitchen_

Now, the **second kitchen**, this have everything mixed, some things and in one cabinet the other half of the ingredient are in another cabinet...

![Second-kitchen-example]()
_Example of the second kitchen_

If you really wanted to make a sandwich, it would be easier to do it in the first kitchen where everything is know where is and not in the second kitchen. After this strange example aboout making sandwichs, we would return to the programming area.

This example, is used to explain what it would be recommended to do when working in big development projects, if you are alone and you "understand" you form of saving things, is great but this also to solve the **hells scripts** as I call it, script with 17,000 lines of code that no one will want to debug.

When developing everything will need to stay in his own box, for example in the following points we are going to talk about the UI, it will be stupid to add a function in the UI script a function that is related to the player, this the most obvious example but others like making a really long script controlling all the workflow of the UI is another. 

If for example the UI is made of a calendar, a textbox and a phone. It would be recommended that every part of this UI has his own script, this because in later development maybe you need to rewrite **only** the calendars functions and not the textbot or phone but because how you made it now you has a long script with a mix of all the functions.

## Making our first object

### Creating the sample object

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


``
