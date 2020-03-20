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

## Keeping score

To give the player a sense of progression, we keep score of how many minions the player has killed (or how many of them have died). We compare that value to an existing highscore, and set a new highscore if we exceed the existing value.

When a new highscore is reached, we display a set of fireworks on the screen, to reinforce that feeling of achieving something. We are currently working on adding a main menu, which will also list the existing highscores.

![](/uploads/fireworks.jpg)

## More minion interactions

Previously, minions were already able to walk into enemy structures and die upon contact. However, they did not inflict any damage. We made some updates, and now the minions properly damage the player's defenses when they run into them. When a structure runs out of health, it dies and gets removed from the game.

## Hands-On

We also were able to build a working version of the game, so you can finally get your very own impressions of the game. You can download it here. Please note that there is no loading screen or main menu yet, you'll start directly into the game.

[Get it here!](https://drive.google.com/file/d/1eczVH7cALpacfkjxVLj7UMX9Knpo5Tg2/view?usp=sharing)

What do you think of the changes we made and the current state of the game so far? Do you have any more ideas on what tools we could give the player to be able to defend himself? Leave your ideas down below in the comment section!