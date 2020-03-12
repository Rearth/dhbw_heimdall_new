---
title: Development Update - Architecture
subtitle: >-
  In our second development update we've made some further progress with out
  game, and will take a deep-dive into our code architecture
category:
  - About Heimdall
author: 'David Waidner, Timo Sickinger'
date: 2020-03-12T20:13:39.136Z
featureImage: /uploads/portals_reworked.jpg
---
A lot has changed since our last dev-blog entry. We made big changes to the environment and further improved our codebase.

![](/uploads/terrain_afar.jpg)

## Environment

The most appearant change is the terrain and the environment of the game itself. We made the terrain smaller, added trees, rocks and other small vegetation features. We also added new models for the bridges, with some lighting in the cliff underneath it. 

The portals have also been reworked, they now have small stone plates underneath, and a set of torches infront. The fog now also spans over one whole half of the map, and stops just before the cliffs.

![](/uploads/portal_close_up.jpg)

## Game Mechanics

The biggest change this week is that minions now interact more with the other objects in the scene. This is one of the bigger challenges, because the minions themselfes are created and managed using the unity ECS (Entity Component System), while the rest of the elements in the game are traditional gameobjects, and interfacing with each other is a difficult task.

![](/uploads/tower_impact.jpg)

However, we were able to find all minions around the impact point of a projectile, and now they will immediatly die and display a small particle effect upon death. We were also experimenting with bodies that fly away form the impact. We achieved that by giving the minions a "rigidbody" component and removing the navagent component. However that once provided us with mediocre resusts, so we decided to just make the minions directly disappear (for now)

## Defences

Most of the changes to the currently implemented towers, are backend changes which are discussed in the following paragraph.

At the moment we are working on "StaticObjects" like walls and a new kind of tower (laser tower). These two are most likely going to be implemented by the next dev-update we are going to post. But we don't want to keep you waiting for too long so here's a little preview of the laserbeam (of course it'll be animated for the finished tower):

![]()



# Architecture

Since we are using a hybrid technology stack of both the traditional unity gameobjects, and the new data-oriented technology stack, we are also using two different architecture sets for our code.

Any code that has anything to do with the minions uses the entity-component system, which is part of the data-oriented technology stack (DOTS). The player defenses and camera-control however use the more traditional gameobject workflow which works using monobehaviours. When using monobehaviours, you are rather free in how you write and architect your code, while the ECS already forces you to write your code in a specific architecture.

![](/uploads/gamedev-2017-aaa-architecture-in-unity3d-59-638.jpg)

As seen in the picture, there's no behaviour in components using the ECS, unlike the monobehaviours. Code is strictly split into data (components) and behaviours/logic (entities). Each system in the ECS is usually just there for one specific aspect of the game, and works on all the entities that have a spefic set of components. 

Currently we have 3 systems dedicated to the pathfinding/navigation of the agents:

* NavAgentSyncSystem: Synchronizes position and rotation of the navagent component with the entity
* NavMeshQuerySystem: Handles all requests for new paths, and calculates a series of waypoints using unity's built-in navigation system
* NavAgentSystem: Moves the navagent component towards it's next waypoint, while doing local obstacle avoidance

For the other logic of the game that interacts with the minions, we have 3 more systems, each dedicated to specific behaviour:

* MinionPhysicsInteractions: Allows the minions to run into player's defenses and die upon impact
* TurretTargetFinder: Finds minions in range of a turret and assign the turrets new targets
* WeaponAOEImpact: Handles the impacts of player defenses projectiles, by killing each minion in a spefic radius around it

When writing ECS-systems, we try to split as much of the work as possible on all available cores, meaning that the code we use there has to be able to be executed in parallel and be threadsafe while doing so. To achieve this, we first gather all data required for the system in the main thread, process the data in a form it can be used in each worker thread (a job), and then execute the actual workload in individual threads, and then process the result of each worker thread again in the main thread.

In more complicate systems, this also leads to more complex job chains, meaning that one job sometimes has to wait for another job or a group of job before it can start.

### ECS Code example

Below you can see a part of the "MinionPhysicsInteraction" system, which starts in the "OnUpdate" method, which runs on the main thread. There we gather all the data required for the worker threads, and then have a total of three different series of jobs. The first series of jobs calculates raycast-data for each minion.

Next we start to actually cast the rays using unity's built-in "Raycastcommand" function, which we give the first series of jobs as dependency.

Then we process the results of the raycastcommand job series using another series of jobs. There we check if the rays hit something, and mark the minions where they did.

Afterwards we wait in the main thread for all the jobs to complete, then delete some of the minions and spawn a particle effect where they died.

At last, we dispose the memory we allocated at the begin of the update method, to avoid memory leaks (all memory that is used in jobs has to be allocated and disposed manually, there's no gargabe collection in ECS)

```csharp
protected override JobHandle OnUpdate(JobHandle inputDeps) {

 var count = minionQuery.CalculateEntityCount();
 var inputs = new NativeArray < RaycastCommand > (count, Allocator.TempJob);
 var hits = new NativeArray < RaycastHit > (count, Allocator.TempJob);
 var toDelete = new NativeArray < Entity > (count, Allocator.TempJob);
 var particlePositions = new NativeArray < float3 > (count, Allocator.TempJob);

 var layerName = LayerMask.NameToLayer("Defence");

 inputDeps = new setupRaycasts() {
  commands = inputs,
   layer = layerName
 }.Schedule(this, inputDeps);

 inputDeps = RaycastCommand.ScheduleBatch(inputs, hits, 1, inputDeps);

 inputDeps = new processResults() {
  hits = hits,
   toDelete = toDelete,
   hitPositions = particlePositions
 }.Schedule(this, inputDeps);

 inputDeps.Complete();

 foreach(var elem in particlePositions) {
  if (!elem.Equals(float3.zero))
   getParticle().doEmit(elem + new float3(0, 1, 0));
 }

 entityManager.DestroyEntity(toDelete);

 toDelete.Dispose();
 particlePositions.Dispose();
 inputs.Dispose();

 return inputDeps;
}

[BurstCompile]
private struct setupRaycasts: IJobForEachWithEntity < Translation, Rotation, MinionData > {
 //[NativeDisableParallelForRestriction]
 internal NativeArray < RaycastCommand > commands;
 internal int layer;

 public void Execute(Entity entity, int index, [ReadOnly] ref Translation pos, [ReadOnly] ref Rotation rot, [ReadOnly] ref MinionData data) {
  var origin = pos.Value + new float3(0, 1, 0);
  var quat = (Quaternion) rot.Value;
  var direction = quat * Vector3.forward;
  commands[index] = new RaycastCommand(origin, direction, 2.5 f);
 }
}

[BurstCompile]
private struct processResults: IJobForEachWithEntity < Translation, MinionData, NavAgent > {

 [DeallocateOnJobCompletion]
 [ReadOnly]
 internal NativeArray < RaycastHit > hits;

 internal NativeArray < float3 > hitPositions;
 internal NativeArray < Entity > toDelete;

 public void Execute(Entity entity, int index, [ReadOnly] ref Translation trans, ref MinionData minionData, [ReadOnly] ref NavAgent agent) {
  var hit = hits[index];
  if (hit.distance < 5 && hit.distance > 0) {
   //has close target, do remove
   toDelete[index] = entity;
   hitPositions[index] = agent.position;
  }
 }
}
```

Hopefully this gave you an idea of how the new ECS works. It really does simplify the creation of code that runs on multiple cores in parallel, which allows us to write the highly performant code we need to keep the game running smooth with the large amounts of minions that we have.

Also, by separating behaviour from data, and using systems that only do one specific job, it helps us keep the code base clean.

## Monobehavior architecture

To code the player's defenses, we use the traditional unity gameobject workflow, which involves the use of MonoBehaviours. They bring a completely different architecture with them and are the "oldschool" way of programming in Unity.

MonoBehaviours allow the GameObject to implement pre-defined functions to realize things like updating and initializing. The use of MonoBehaviours in our project is the only logical choice, because every Tower has to be initialized and updated.

The implementation of the Defence-System relies heavily on abstraction. This means that, for example, a fire tower is "DefenceObject" but can be specified as an object of the class "TowerFire". This allows us to use the concept of polymorphism to call functions on all kinds of "DefenceObject" and thus makes the code a lot cleaner and easier to expand and mantain.

To visualize this concept, the following UML-Class-Diagramm was generated straight out of our code:

![ClassDiagramm](/uploads/classdiagram6.png "ClassDiagramm")



## Now it's your turn!

We are always open for criticism and new ideas, so please feel free to write the down below.

To be more specific we have two questions for you:

\- Would you have done the architecture in any other way? If yes, why?

\- What kinds of towers and other buildable objects would you like to see in the finished game?