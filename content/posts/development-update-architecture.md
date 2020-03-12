---
title: Development Update - Architecture
subtitle: >-
  In our second development update we've made some further progress with out
  game, and will take a deep-dive into our code architecture
category:
  - About Heimdall
author: 'David Waidner, Timo Sickinger'
date: 2020-03-12T20:13:39.136Z
featureImage: /uploads/tower_impact.jpg
---
A lot has changed since our last dev-blog entry. 

## Environment

The most appearant change is the terrain and the environment of the game itself. We made the terrain smaller, added trees, rocks and other small vegetation features. We also added new models for the bridges, with some lighting in the cliff underneath it. 

The portals have also been reworked, they now have small stone plates underneath, and a set of torches infront. The fog now also spans over one whole half of the map, and stops just before the cliffs.

## Game Mechanics

The biggest change this week is that minions now interact more with the other objects in the scene. This is one of the bigger challenges, because the minions themselfes are created and managed using the unity ECS (Entity Component System), while the rest of the elements in the game are traditional gameobjects, and interfacing with each other is a difficult task.

![](/uploads/tower_impact.jpg)

However, we were able to find all minions around the impact point of a projectile, and now they will immediatly die and display a small particle effect upon death. We were also experimenting with bodies that fly away form the impact. We achieved that by giving the minions a "rigidbody" component and removing the navagent component. However that once provided us with mediocre resusts, so we decided to just make the minions directly disappear (for now)