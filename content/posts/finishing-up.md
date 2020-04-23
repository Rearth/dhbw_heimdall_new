---
title: Finishing up...
subtitle: ... for now!
category:
  - About Heimdall
author: David Waidner, Timo Sickinger
date: 2020-04-23T21:00:00.000Z
featureImage: /uploads/portal_final.jpg
---
This post will be our final post for now...

But don´t be disappointed, we have got alot to share with you this week. So keep reading and learn about all the new things we implemented over the last two weeks.

# Development-Update

In the last two weeks we did not implement that many large features, but we did alot of bugfixing and finishing things up. None the less we also have a few new things we would like to share with you in the following lines.

## UI update

We updated the UI in several parts of the game to give the player a more visual experience while playing. But most importantly we have a new menu-screen with options for controlling and saving the music- and the soundeffects-volume.

### Options menu

In the options-menu it is possible for the player to control the volume of the music and soundeffects seperately. If the button apply is clicked, the configured options will be saved in the registry of the computer. This allows us to load these options back in to the game and keep the volume at the same level between game sessions.

![](/uploads/options.jpg "Options-Screen")

### Control-Panel and Coin-Display

To give the player a better visualization of the controlls and also make them easier to read, we updated a few of the controlls and replaced the previous text with images of the actual buttons you have to press. This makes is much easier to get a grasp of the controlls if you are playing the game for the very first time.

Since there was now way of telling how much coins you have left to build, we also implemented a simple display in the HUD which represents the amount of coins you currently have at your disposal.

![](/uploads/ui1.jpg "NewUI")

### Range and Cost of Towers/Upgrades

One of the most important pieces of information in tower defence games is the range of the tower. Until now our towers just shot at enemies and the player had no idea how far the tower was able to shoot. But now we visualize the range with a very flat cyclinder object. This way the player knows where to build a tower that is very effective.

In addtion to the range, the cost of the tower is now also displayed while in building-mode. The cost of an upgrade is also visualized if the tower is selected.

![](/uploads/range_costs.jpg "RangeBuilding")

![](/uploads/upgrade.jpg "UpgradeCost")

## Music and sound

Of course a game is not complete without music and sound. We added two different pieces of music. One for the menus and one for the game itself. But of course soundeffects are also a very important part of a game, so we added a few soundeffects for building a tower, shooting a projectile and the impact of a projectile with the ground or an enemy.

As mentioned above the music and soundeffects can be controlled seperately via the options-menu and can be stored in the so called PlayerPrefs to load and save them at anytime, which results in a great consistency across several game sessions.

## Balancing

Using the data we gathered from our test runs and processed later on, we rebalanced almost all values in the game. We were able to see if a towers is too strong/weak, and so we adjusted the costs of all buildings, and altered their hp and build costs.

This allowed us to make the gameplay feel better, staying alive in the game now is a real challenge. The player can try to invest into the future by building gold mines already early on, but this will limit the budged remaining for the defenses. Also, the player can try to block paths using walls, but this only works as a short-term solution, since the wall will quickly run out of health points, and the minions will also find a way around the walls after a while.

## Analytics

Over the past few days we had couple of people play our game. From them we gathered a few data-points which we analyzed and came to some conclusions about the performance of the game and the playstyle of the players themselves. 

In the following lines we want to share this data with you and tell you about the conclusions we made about them.

### Average tower distance to tower-count

![](/uploads/diag_c.jpg)

As you can see in the diagramm above, the games in which the players placed the towers closer to the castle, went much better, since they were able to afford more towers in general. Of course there are not enough datapoints to tell if the best tactic is to build all towers close to the base but it`s atleast a trend that the players discovered.

### Usage of the different tower types

![](/uploads/diag_b.jpg)

In the diagram above, you can see the different tower kinds, with the bars indicating their distance to the player's castle. This confirmed our expectations. Most players tend to place the archers on/in front of the castle to act as a "last line of defense", while the bigger towers are usually placed much further out, probably inbetween the different minions lines.

## Final work hours

We already published the Link to the google sheet we're using to track the amount of work we've put into the project. The detailed [summary can be found here](https://docs.google.com/spreadsheets/d/1-k8MbfULlLRi6_MjK0al4zIdhj9PC8CfBLr8aLHBsTI/edit#gid=0). In total we've worked over 92 hours on the project.

David: 42:20 hours

Timo: 50:12 hours

## Lessons learned

We learned a ton of new stuff over the course of this project. Since we started this as a new game from scratch, we were able to experiment with many new technologies and aspects of software engineering. Also, working together as a small team of two programmers brought some new challenges.

The usage of the Data-oriented technology stack (DOTS) taught us a completely new way of architecting our code. Instead of writing traditional object-oriented code, we completed some aspects of the game as "data-oriented" code, which is a whole new approach to modern programming. It took some time to get used to it, but made it a lot easier to split the computing tasks on the game on different cores, and keep both the data and logic separate, which also resulted in more clean code in general. We learned a lot about parallelization and optimization of our code.

Watch our [trailer on youtube](https://youtu.be/Yy-Vg-5zkf4)! If we got you interested in the game, you can download our[ final release here](https://developer.cloud.unity3d.com/share/share.html?shareId=-kdIS3Y6nH).