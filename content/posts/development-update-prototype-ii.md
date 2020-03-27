---
title: Development Update - Prototype II
subtitle: >-
  We further improved the visuals of our project, fixed some bugs and did some
  changes to the lighting and the quality settings of our project, resulting in
  a more pleasing looking environment, while also getting a boost in
  performance.
category:
  - About Heimdall
author: 'David Waidner, Timo Sickinger'
date: 2020-03-26T19:33:46.710Z
featureImage: /uploads/fortress_initial.jpg
---
We further improved the visuals of our project, fixed some bugs and did some changes to the lighting and the quality settings of our project, resulting in a more pleasing looking environment, while also getting a boost in performance.

## Terrain Changes

We removed all vegetation from one side of the bridge (the one where the player's fortress is). This will give the player a better overview of the current situation, and give the player a lot more space to build, since there's no more forest blocking him. We also updates the textures on the terrain itself, and updated the tiling settings, resulting in a lot more details being visible. The the terrain textures can unleash the full potential of their normal, which earlier were too small to be noticable due to the tiling settings.

![](/uploads/terrain_afar_new.jpg)

Also we added a small castle keep as the player's "main base". The minions will target this castle, and the game will be over when that keep get's destroyed. It is now built into the mountainside, with walls on only one side, and the mountain active as another wall to keep it save.

![](/uploads/fortress_initial.jpg)

## Lighting

We noticed that shadows were barely visible in our game. Upon further inspection, we noticed that the default render distance for shadows was set to only 50 meters, which was way too small for our game, since the camera doesn't really get close to any objects. We set it to 1000 meters, and that made the game look much better.

![](/uploads/terrain_tiled.jpg)

We also started with lightmaps, which allow us to precompute the shadows and lights of the static objects in our scene, which should give us even better looking lights and shadows, since the engine is able to calculate them in advance. Unity actually traces the lights and simulates multiple bounces off of nearby surfaces. The results will be baked into the materiels of the objects in the scene, and do not need to be recalculated during runtime, resulting in superior perfomance and 

## Tower Effects

To improve the way our towers and defences are being built, we made a new Shader to visualize the process of building. The shader uses socalled "SimpleNoise" to fade the building into existence. Sadly the shader and the respective material don't work on defences at the moment. But here is a short preview to show you how it is going to look:

![](/uploads/dissolvemat.jpg)

## Other Improvements

Our Unity Editor started to act really sluggish, and it took multiple minutes to even start up the editor. We fixed that cleaning up our assets using [this asset cleaner](https://github.com/unity-cn/Tool-UnityAssetCleaner). By applying the asset cleaner, we were able to remove ~650mb of files in our project, making the editor run a lot more smooth again.

You can get your hands on the current version using [this link](https://developer.cloud.unity3d.com/share/share.html?shareId=-yQjLOKIiS).

## Questions for you

We are still thinking about the storyline for the project. What kind of story could be behind this project? What could be reasons for the castle being attacked by those minions?

Also, what kind of economy could fit into the project?