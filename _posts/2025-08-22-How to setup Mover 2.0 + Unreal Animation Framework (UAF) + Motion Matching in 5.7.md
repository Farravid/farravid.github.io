---
title: How to setup Mover 2.0 + Unreal Animation Framework (UAF) + Motion Matching in 5.7
date: 2025-08-22 12:37:00 +0200
categories: [Unreal Engine, Animation]
tags: [gameplay, animation, tutorial]    # TAG names should always be lowercase
lang: en
media_subpath: /assets/img/mover-uaf-motionmatching/
---


About two months ago, the technical demonstration of The Witcher 4 at Unreal Fest showcased the next-generation animation system of the Unreal Engine (Unreal Animation Framework, hereafter referred to as UAF, while the previous animation blueprint system will be referred to as ABP). This sparked my strong curiosity, and I felt it was time to dive into understanding this system.

This article will analyze the system from a architecture perspective, primarily introducing its components, the meanings of various types, and their logical relationships. I hope this will help everyone grasp and get started with this new animation system, but it will not cover details such as animation blending calculations or animation retargeting.