---
layout: project
type: project
image: images/py title.png
title: Collaborative Project- Video Game
permalink: projects/pyfighter
# All dates must be YYYY-MM-DD format!
date: 2018-12-28
labels:
  - Python
  - Pygame
  - Unity
summary: A collaborative project to make a side-scrolling space shooter called "The Last PyFighter." Our team, "Try Force," created this game in a very short amount of time.
---

<figure class="video_container">
  <video controls="true" allowfullscreen="true" poster="../images/pyfighter title 2.png">
    <source src="../images/pyfighter demo.mp4" type="video/mp4">
  </video>
</figure>

*An extract from the Last Pyfighter instruction manual:

The Year is 30XX
The Human Race is under attack.
Using stolen alien technology humanity developed The Pyfighter.
You have been tasked to fight off the hordes of the Zalgrons.
Good Luck...

To control the Pyfighter you use the arrow keys to move around the screen. Space Bar fires the LAZOR Cannon at the alien scum. 

As a human with little regard for alien life (as they have none for yours), you have been equipped with experimental smart bombs that can instantly destroy the drone ships sent to bring you down. 

Beware: if you kill enough aliens, you will attract the attention of the alien destroyers, who will prove to be a tougher match. 

This game was loosely inspired by Galaga and other such arcade games from the 80s. The art is inspired by sci-fi entertainment from that era and was drawn by Jes. 

The game is a wave-based, side-scrolling shooter with bullet-hell elements. The player has omnidirectional 2D control around the screen. The player has access to two weapons: a basic straight-line firing gun and a screen clearing bomb. Powerups were implemented to allow for higher level play options such as resource management. 

Life and point systems are implemented to allow rankings of each game play run. These are added to a high score file after assigning the player name after each run. 

The High Scores are also displayed on game over. 

A boss wave was added every 4th wave to provide additional challenge and variation, as well to reward the player with powerups they may not have received from the random spawns. 

There are some quality of life implementations in the game as well: there is an option to pause the game loop mid-play, as well as quit the game without needing to use the mouse. There is also a start screen that explains how to play the game without the needing to read the readme. 

Sounds were taken from grsites.com 
Music was taken from dl-sounds.com*

My contributions were largely asthetic. 

I created all of the graphics, which were hand-drawn on an iPad and edited with Autodesk. I created the graphics for and layout of the title screen. The ships were inspired quite a bit by Battlestar Galactica, as I imagine is apparent. Originally, the hero ship would change to a 2.5D view of the ship when moving vertically, but this was changed during refactoring. There are two version of alien ships: one without a shield and one with. I drew and implemented a simple parallax background, to give the screen the illusion of depth.

<div class="ui medium rounded images">
  <img class="ui image" src="../images/pyfighter title.png">
  <img class="ui image" src="../images/pyfighter wave.png">
</div>

I created and implemented all of the animations, which include animated thrusters for both the hero and alien ships, the two power ups, and explosions. The powerups (extra life and bomb) were designed to stand out, but not create "busy" distractions for the player. For the "boss" enemies, I drew the ship in various states of destruction, which would alter the ship as its health bar diminished. The final state, the boss is floating aimlessly in space with its red eye put out. This was actually done on the final day, a few hours before the project was to be completed. I was surprised how well it turned out.

<img class="ui medium centered rounded image" src="../images/pyfighter boss 1.png">

<div class="ui small rounded images">
  <img class="ui image" src="../images/pyfighter boss 2.png">
  <img class="ui image" src="../images/pyfighter boss 3.png">
  <img class="ui image" src="../images/pyfighter boss 4.png">
  <img class="ui image" src="../images/pyfighter boss 5.png">
</div>

As the art was a significant part of the contribution (and I was most artistically inclined), I researched quite a bit on converting different graphic types in the code, to keep the game running smoothly. I also researched and tested how the animation code would affect performance and how it could be adjusted optimally.  I also found and implemented the sounds and music.

For the code, I spearheaded the second refactoring and use of in-built classes. We had made three versions of the game. The first refactor set us up to use OOP style, but none of us really understood the use of Groups (a class in-build to Pygame). I studied up on it, as it seemed to be the answer to a lot of little things nagging at my brain. During the first refactor, hero and enemy hitboxes, collision detection, powerup collection, and lot of other things were created with very clever and complex code. I was interested in something more direct and versatile. In researching two in-built classes to Pygame (Sprites and Groups), I realized, when used correctly, these things are much more simply and elegantly implemented. I took what I had found back to the group, we wrapped our collective brain around it, and were able to produce the second refactor.

[The project's GitHub repo](https://github.com/Demi-hero/UoN_Game_Project).
Try Force was [Peter](https://github.com/ExcessGravitas), [Nathan](https://github.com/Demi-hero/), and myself. They were really lovely to work with.
