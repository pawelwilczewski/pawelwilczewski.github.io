---
title: "3D Skinning Tool"
layout: post
categories: University
tags: C++ OpenGL
---

![Skinning Tool Thumbnail](/assets/img/skinning-tool/thumbnail.png){: width="70%" }

<h2>{{ page.title }}</h2>

3D mesh weight-painting tool for tweaking appearance of skeletal animation.


3D mesh skinning tool I implemented for my final year dissertation project during my time at the University of Leeds.

Special attention was paid to separation of concerns, single responsibility, easy extendability and accurate
abstractions.

Some functionalities include:
- Importing and exporting `gltf` skeletal and static mesh models.
- Tools for editing and previewing skinning weights in real-time.
- Support for importing and playing back animations.
- Scene hierarchy with selectable entities.
- Selecting bones directly in the viewport allowing for rapid iterations.
- Fully resizable and dockable UI.

{% include embed.html url="https://youtube.com/embed/nDsgmSxf01k" %}