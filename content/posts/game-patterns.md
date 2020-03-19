---
title: Game-Patterns
subtitle: and a small dev-update
category:
  - About Heimdall
author: 'David Waidner, Timo Sickinger'
date: 2020-03-19T19:03:36.345Z
featureImage: /uploads/retro-gaming-pattern.jpg
---
This week our main focus was targeted on recognizing and describing game-patterns for our game. We managed to find at least three different ones we want to tell you about in this weeks blog-post.



## Building

The first pattern we recognized was of course the building-aspect of our game. As a player you can build multiple objects, such as towers or walls. The main goal is of course to build as effective and efficient as possible to protect your base from enemies. To give feedback to player if an object is placeable or not the material of the object changes to highlight it accordingly.



## Highscore

To track the progress of the player, the best score is saved and displayed in the main menu. This can also be used to show off to friends or compare scores with them. This can also be a factor for long-term engagement because freinds can challenge eachother again and again to beat the newest highscore.



## Survival

The main objective of our game is also the main pattern we discovered: Survival. The goal of our game is to protect your base for as long as you can from an increasing amount of enemies. Of course the difficulty will scale over time so it gets harder and harder the nlonger you play.



# Development-Update

Of course we didn't just brainstorm the whole week. we also added some features and fixed a few bugs we noticed. in the following paragraphs we will explain and show to you what we chnaged this week.



## Static-Objects

As we promised last week we implemented static buildable objects. To start off we implemented a stone wall which is ment to redirect the enemies and force them along a chosen path. To realize this we added an "Obstacle" component to the wall and bake the Navmesh at runtime to manipulate it and recalculate the paths of the enemies.

![](/uploads/stonewall.jpg)