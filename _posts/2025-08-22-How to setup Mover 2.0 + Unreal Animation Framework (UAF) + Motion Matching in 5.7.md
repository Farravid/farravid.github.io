---
title: How to setup Mover 2.0 + Unreal Animation Framework (UAF) + Motion Matching in 5.7
date: 2025-08-22 12:37:00 +0200
categories: [Unreal Engine, Animation]
tags: [mover, uaf, motion matching]    # TAG names should always be lowercase
lang: en
media_subpath: /assets/img/mover-uaf-motionmatching/
image:
    path: banner.jpg
---

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