---
title: How to setup Mover 2.0 + Unreal Animation Framework (UAF) + Motion Matching in 5.7
date: 2025-08-22 12:37:00 +0200
categories: [Unreal Engine, Animation]
tags: [gameplay, animation, tutorial]    # TAG names should always be lowercase
lang: en
pin: true
media_subpath: /assets/img/mover-uaf-motionmatching/
image:
    path: /assets/img/mover-uaf-motionmatching/banner.jpg
---

#

This article will explore how to connect three of the most cutting-edge technologies from Epic Games in Unreal Engine. The future is here 🚀

# Useful knowleadge to have
- [What is Mover 2.0](https://unrealstack.com/what-is-ue5-character-mover-2-0/)
- [What is UAF](https://dev.epicgames.com/community/learning/knowledge-base/nWWx/unreal-engine-unreal-animation-framework-uaf-faq)
- [What is Motion Matching](https://dev.epicgames.com/documentation/en-us/unreal-engine/motion-matching-in-unreal-engine)
- [Deeper talk about UAF: How the system is built, why, reasons behind it](https://www.youtube.com/watch?v=0X6amtHcrUE&t=1190s)

> This example was made using Unreal Engine 5.7 from source code. You may find issues trying to implement this in older versions.
{: .prompt-warning }

# Plugins requirements

In order to achieve this, you need to enable some plugins that we will use.

> I'm assuming you know which plugins you should enable for Motion Matching since this is not the experimental part of the article
{: .prompt-tip }

## Mover plugins

![alt text](mover-plugins.png)

I enabled all of them but I think the squared ones are the most relevant.

## UAF plugins

![alt text](uaf-plugins.png)

# Mover setup

First, we are gonna dive into the Mover plugin. The setup is pretty straight-forward since we are gonna use some examples from Epic and the configuration is pretty similar to the old CMC (Character Movement Component).

Even though, the concept is quite different and how it is handled internally, the config remains the old CMC.

First things first, we are gonna create a BP class inheriting from `BaseAnimatedMannyPawn`  

![alt text](bp-create.png)

Then you can jump in the created BP and tweak/discover as much as you want the new Mover plugin. There are some similar properties such as MaxSpeed, etc...

![alt text](mover-vars.png)

The setup for Mover is pretty much ready, you will be able to throw your created BP into a level and move/jump freely.

# UAF & Motion Matching setup

This is where the thing gets more interesting.

Will try to keep things simple since it's a first approach and I'm not super knowledgeable on the topic yet.

## UAF main pieces

The new UAF system is composed by many pieces and will be more complete and powerful that it is right now. For now, we will focus on the main pieces to setup a basic system.

> You can find these assets under `Animation > Animation Framework` when creating a new asset
{: .prompt-tip }

* **Animation Graph**: similar to the AnimGraph of the old ABP. Will handle the animation logic in a more data-composition way
* **System**: think of it as the EventGraph part of the ABP. 
* **Workspace**: it seems that the new UAF will have a lot of assets to handle at the same time, so the workspace is like an editor sandbox where you can throw your different systems, shared variables or graphs and work together, pretty cool.   

![alt text](pieces.png)


## UAF setup: AnimNext

We need to add an `Actor Component` to our previous BP created in order to enable UAF/AnimNext.

Look for `AnimNext` and make sure to assing your created `UAF system`

![alt text](animnext.png)

> Make sure also to disable entirely animation from the SkeletalMeshComponent, otherwise AnimNext/UAF won't kick in!
{: .prompt-warning }

![alt text](disable.png)

## UAF setup: Workspace

As mentioned the workspace is just like an editor sandbox.  
So before anything, make sure to create the 3 assets (Workspace, System, Graph) and add the System and the Graph to the workspace like shown in the image.

![alt text](workspace.png)

## UAF setup: System

This is where our logic will live. As you can see, for the basic setup, the logic is pretty simple.  

1. Generate the reference pose when initializing the system
2. Generate the trajectory that we will use later for Motion Matching using the Mover component
3. On update, we run the graph and then, with the result pose obtained from the graph, we write the pose to the system.

![alt text](system.png)

### New variable bindings!

You may have noticed how I'm using the Mover Component reference without actually setting it on the system. Unreal added a pretty cool way of retrieving components and other variables using bindings, like this:

![alt text](bindings.png)

This seems the new way of getting references to components or the owner actor of the system. Which I really like.

## UAF setup: Graph

> Not sure why the graph is like "not active" (opacity not set to 1). Probably some WIP stuff
{: .prompt-tip }

The basic setup is also straight-forward on the graph side. Just evaluating a Chooser Table and feeding the Motion Matching node with the databases and the trajectory previously calculated. 

![alt text](graph.png)

# UAF & Motion Matching showcase

If you are lucky and the setup is still working the same way, you should see your character doing some Motion Matching stuff, not consuming `GameThread` and using the cool Mover 2.0!

[Here's a litte showcase on my LinkedIn 😎](https://www.linkedin.com/posts/farravid_uaf-mover-motionmatching-activity-7363892094509211649-krtB?utm_source=share&utm_medium=member_desktop&rcm=ACoAACwyukMBzcsuU4n2ZFaWBDgbHdI9pxZsg_E)

# Bonus: set variables from `AnimNext` component

You can send variables to your UAF system through the `AnimNext` component on your pawn.

![alt text](set-variables.png)

# Bonus: a more technical post about UAF on 5.6
[Big thanks to RemRemRemRe for the post about UAF on 5.6, with a more technical perspective of the new system](https://remremremre.github.io/posts/My-understanding-of-Unreal-Animation-Framework-in-5.6/)
