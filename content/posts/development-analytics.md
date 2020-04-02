---
title: Development - Analytics
subtitle: analyzing...
category:
  - About Heimdall
author: 'David Waidner, Timo Sickinger'
date: 2020-04-02T17:50:45.507Z
featureImage: /uploads/analysis.jpg
---
This week we set up the hooks to analyze the data of our game. The goal is, to improve the gameplay and feeling of our game with the data we are going to collect from our users (No worries: we are bot tracking personal data).

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



## Question-Time

This week we want to know from you:

* Do you have ideas on what to track in the future?
* Should we share the collected data in a future post?