---
title: "Node Editor"
layout: post
categories: Commercial
tags: C# Blazor
---

![Node Editor Thumbnail](/assets/img/node-editor/NodeEditor.png)

<h2>{{ page.title }}</h2>

General-purpose, easily extendable node-editing web application developed as contract work.


Contract project I developed for Jaworski Software Solutions Ltd as the main full stack developer in 6 months
(part-time).

Main features and design:
- Fully functional and feature-rich node editing.
- Copy & paste, undo & redo.
- Easy extendability and integration with external APIs (SDXL image generation shown in the video below).
- Nodes defined as methods, supporting dependency injection - adding new functionality could not be simpler.
- Automatic computed result caching.
- Optimal parallel execution.
- Clean architecture & clean code.
- Full persistence.
- Theme support.

Tech stack:
- ASP.NET Core
- Blazor
- Entity Framework Core
- TailwindCSS
- PostgreSQL

{% include embed.html url="https://www.youtube.com/embed/1TASg7uvFLg" %}

![Node Editor Thumbnail](/assets/img/node-editor/light-theme.png){: width="70%" }
*Light theme editor view*