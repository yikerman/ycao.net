---
title: "Optimal Gravity Turn Profile in KSP"
date: 2025-04-07 00:30:00 +0800
tags: [physics]
math: true
---

Getting rockets into orbit in KSP is easy; however getting them into orbit gracefully is actually quite hard since Kerbin is significantly smaller than Earth, but the atmosphere is not much scaled down. This resulted in the differences to the real world in which most of the maneuvering is done in the vacuum of space. This post tries to build a simplified model of the gravity turn maneuver in KSP and find the optimal trajectory.

The model is based on the following assumptions:

- Kerbin has a uniform $G$ ($\text{m}\text{s}^2$).
