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

<video width="720" height="405" controls>
    <source src="../images/pygame demo.mp4" type="video/mp4">
</video>

### *An extract from the Last Pyfighter instruction manual:*

*The Year is 30XX*
*The Human Race is under attack.*
*Using stolen alien technology humanity developed The Pyfighter.*
*You have been tasked to fight off the hordes of the Zalgrons.*
*Good Luck...*

*To control the Pyfighter you use the arrow keys to move around the screen. Space Bar fires the LAZOR Cannon at the alien scum.*

*As a human with little regard for alien life (as they have none for yours), you have been equipped with experimental smart bombs that can instantly destroy the drone ships sent to bring you down.*

*Beware: if you kill enough aliens, you will attract the attention of the alien destroyers, who will prove to be a tougher match.*

*This game was loosely inspired by Galaga and other such arcade games from the 80s. The art is inspired by sci-fi entertainment from that era and was drawn by Jes.*

*The game is a wave-based, side-scrolling shooter with bullet-hell elements. The player has omnidirectional 2D control around the screen. The player has access to two weapons: a basic straight-line firing gun and a screen clearing bomb. Powerups were implemented to allow for higher level play options such as resource management.*

*Life and point systems are implemented to allow rankings of each game play run. These are added to a high score file after assigning the player name after each run.*

*The High Scores are also displayed on game over.*

*A boss wave was added every 4th wave to provide additional challenge and variation, as well to reward the player with powerups they may not have received from the random spawns.*

*There are some quality of life implementations in the game as well: there is an option to pause the game loop mid-play, as well as quit the game without needing to use the mouse. There is also a start screen that explains how to play the game without the needing to read the readme.*

*Sounds were taken from grsites.com*  
*Music was taken from dl-sounds.com*

My contributions dealt largely with the aesthetics of the game, both artistically and programmatically. As mentioned in the introduction text, the game drew inspiration from retro pop culture.  

I created all of the graphics, which were hand-drawn on an iPad and edited with Autodesk, including:
- graphics for and layout of the title screen
- hero ship, bullets, and thruster fire
- enemy ships, shields, bullets, and thruster fire
- boss ship and stages of destruction
- hero and enemy death explosions
- powerups (extra life and bomb)
- background

<div class="ui large centered rounded images">
  <img class="ui image" src="../images/pyfighter title.png">
  <img class="ui image" src="../images/pyfighter wave.png">
</div>

## Player and Enemies
The hero and enemy ships were inspired by Battlestar Galactica, as I imagine is apparent.

### Hero

Originally, the hero ship would change to a 2.5D view of the ship when moving vertically (as shown on the title screen), but this was changed during refactoring.

Animated fire with a low level of transparency emanates from the hero ship's engines if the player is moving forward, but it stops if moving backward. There is visual and audio feedback to indicated shots fired and hero ship destruction.

### Aliens
There are three types of alien ships: shielded, unshielded, and a shielded AI. The non-AI aliens follow a straight path across the screen, while the AI aliens attempt to line up with the player to shoot them. As the alien ships are moving ever forward, fire with a low level of transparency always emanates from alien ship engines.

Depending on the level of protection, the player needs to successfully shoot the aliens a different number of times (e.g., if the enemy is shielded, the player needs to shoot once to destroy the shield and a second time to destroy the ship). There is visual and audio feedback to indicate shields hit/destroyed and ship destroyed.

### Boss
For the "boss" enemies, I drew the ship in various states of destruction, which would alter the ship as its health bar diminished. Initially, the boss ship moves around the right side of the screen, firing bursts of multiple bullets and tracking the player's position. As the boss is damaged, the boss' health bar depletes, and there is visual feedback for three stages of damage. On the fourth stage of damage, the boss ship floats aimlessly in space, now using the entire screen and making the giant ship itself a danger to the hero. In the final stage of damage, the glowing red eye of the boss goes out before it is finally destroyed.

All of this was actually done on the final day, a few hours before the project was to be completed. I was pleasantly surprised how well it turned out.

<img class="ui large centered rounded image" src="../images/pyfighter boss 1.png">

<div class="ui small centered rounded images">
  <img class="ui image" src="../images/pyfighter boss 2.png">
  <img class="ui image" src="../images/pyfighter boss 3.png">
  <img class="ui image" src="../images/pyfighter boss 4.png">
  <img class="ui image" src="../images/pyfighter boss 5.png">
</div>

### Powerups
There are two powerups available randomly to the player: an extra life and a bomb. The extra life simply adds an extra try to the players available lives. The bomb will damage all ships on the screen (for alien ships, it will destroy all visible ships, regardless of whether they are shielded. For boss ships, it will deal substantial damage but not automatically destroy it (unless the boss' health is already so low)).

The powerups were designed to stand out, but not create "busy" distractions for the player. The extra life is a smaller version of the hero ship with a flashing "+1" above it. The bomb is shown as a metal case with a red swirling interior. Both powerups can be collected by coming into contact with them.

## Field of Play

I implemented a simple parallax background, to give the screen the illusion of depth and set the scene in a familiar "outer space" atmosphere.

Aside from the active audio and visual feedback from the hero and enemy ships, there are also text elements. These serve to inform and/or ready the player:
- score: the current score
- wave: which enemy wave is on (every fourth wave is a boss wave)
- bombs: the number of bombs the player has available
- lives: the number of tries the player has remaining
- enemies reinforcements: how many more enemies are left in the current wave
- health bar (boss wave, only): how much health the boss ship has remaining
- high score screen displayed after all lives are depleted (opportunity to input name if ranked)

## Code
I was lucky to have such talented coding partners. We spent a lot of time paired (or... tripletted?) coding. I was often the rubber ducky— able to look at code to debug and find errors or talk through code to help develop ideas that would help us reach the goal.

### Refactoring
I spearheaded the second refactoring of the games' code and use of in-built classes. We made three versions of the game, in the end. The first refactor set us up to use OOP (Object Oriented Programming), but we were each learning Pygame in a very short amount of time and did not understand all of the possibilities right off the bat.

During the first refactor, hero and enemy hitboxes, collision detection, powerup collection, etc. were created with very clever and complex code. Thus, initially we didn't have form-fitted colliders, which created (non-fatal) problems in the game play. For example, due to ill-fitted colliders and hitboxes, the player and enemies could be destroyed by hitting seemingly arbitrary points nearby or missed shots that look like they *should* land.

I was interested in something more direct and versatile. In researching possibilities, I came across documentation for two in-built classes to Pygame: Sprites and Groups. I realized, when used correctly, hitboxes and collision detection can be more simply and elegantly implemented.

I took what I had found back to the group, we wrapped our collective brain around it, and were able to produce the second refactor. I think we produced something really nice, especially for each of our first games and the time constraints (~1 month).

### Aesthetic Considerations
As much of my overarching contribution was the aesthetics, I additionally researched converting different graphic types in the code to keep the game running smoothly.

All of the animations are done programmatically, so I also researched and tested how different approaches to this would affect performance and how it could be adjusted for optimal performance.

[The project's GitHub repo](https://github.com/Demi-hero/UoN_Game_Project).
Try Force was [Peter](https://github.com/ExcessGravitas), [Nathan](https://github.com/Demi-hero/), and myself. They were really lovely to work with.
