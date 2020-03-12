---
title: What is Heimdall?
subtitle: >-
  Heimdall is a Software-Engineering project made for the 'Games' Class at the
  DHBW Karlsruhe.
category:
  - About Heimdall
author: David Waidner
date: 2020-02-27T15:02:27.811Z
featureImage: /uploads/nikola-damjanov-nordeus-unite-demo-005.jpg
---
Heimdall is a Software-Engineering project made for the 'Games' Class at the DHBW Karlsruhe.

The Project is being worked on by two people. Is is a single-player-game made with Unity3D. The targeted platform(s) are mainly desktop PCs right now.

# The Game

The goal of the game is to build a castle with fortifications and units to defend it. The castle will be under attack by thousands of evil minions, brought into the world by unknown, nefarious forces.

![](/uploads/nikola-damjanov-nordeus-unite-demo-009.jpg)

The goal of the player is to build as many defenses as possible, thus holding the castle for a longer time. There is only one 'level' in the game, which can be started multiple times, each time with the goal of surviving for a longer time (basically a score). The highscore will get saved.

# Technology

We will be using Unity3D as Framework/Editor for the Project. Collaboration will be done using Unity's 'collab' feature.

Since we want to have huge amounts of enemies in the game at the same time (thousands!) we will be using the new Unity DOTS stack. The most relevant feature of this will be the new 'Entity Component System' (ECS). This allows us to program the game in a more efficient way. ECS promises multiple advantages:

* Extremly performant code
* Easier to read
* Easier to reuse code
* Burst Compiler

We will see if it can hold those promises in a later stage of the project.