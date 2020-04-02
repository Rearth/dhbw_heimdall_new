---
title: Development - Analytics
subtitle: analyzing...
category:
  - About Heimdall
author: 'David Waidner, Timo Sickinger'
date: 2020-04-02T17:50:45.507Z
featureImage: /uploads/analysis.jpg
---
This week we set up the hooks to analyze the data of our game. The goal is to improve the gameplay and feeling of our game with the data we are going to collect from our users (No worries: we are not tracking personal data).

To track all the data we need, we are using the built-in Unity-Analytics service. This allows us to view the collected data inside of an online dashboard and visiualize it with graphs.

## The Hooks - Gameplay

* The achieved Score
* The highest Score
* The amount and the kind of DefenceObjects that were placed
* Won the Game?
* Skipped the Intro? If yes: at which point?

## The Hooks - Performance

Of course a huge part of our game is the new ECS System which is made to be extremely performant. So we also want to track the average performance of the game and, in relation to the performance, the amount of time the game lasted. This will help us the improve the performance and therefore get more people to be able play the game.

* average FPS
* length of the game

## New Content

As always, we also added some new content to the game. We now have a main menu which can be used to start the game:

![](/uploads/menu_first.jpg)

At the begin of the game we now also show a short cutscene that introduces the player to the game. The UI has also been improved, with a health bar on the top right showing the current HP of the player's base, and a big animated counter on the top that shows the current minion kill score. Next to that you also see the last highscore.

![](/uploads/score_display.jpg)

We also added  a new unit the player can use to defend his base against the minion hordes: the archer. He can be placed like any other defense building, but he can also be built on some of the existing walls (or newly placed ones).

Archers will shoot arrows towards the minion armies, and are very useful for picking off targets that have made it past your bigger but slower aiming turrets. The archers are very accurate at a close distance, but have a hard time at hitting targets further away.

To allow the players to use large amounts of archers (to achieve huge movielike arrow storms) we implemented the arrows of the archers using the ecs system. Each arrow is it's own entity, and the flight path for the entity will be calculated when launching it, and is based on elliptical curves. Once the arrows reach a certain height (towards the end of their flight) we use batched raycasts to detect collisions with enemy minions, and apply damage to the first minion the ray finds. If no minion is found, the arrow will just get stuck in the ground, where it will stay for a few seconds after being removed from the game.

![](/uploads/archers_on_wall.jpg)

You can also download the current version of the game [using this link](https://developer.cloud.unity3d.com/share/share.html?shareId=W19pwQr3iB). Please give it a try and leave us some feedback in the comments.

## Question-Time

This week we want to know from you:

* Do you have ideas on what to track in the future?
* Should we share the collected data in a future post?