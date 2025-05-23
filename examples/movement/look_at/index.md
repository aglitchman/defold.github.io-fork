---
author: Defold Foundation
brief: This example shows how to rotate a game object to look at the mouse cursor
category: movement
layout: example
name: Look at
path: movement/look_at
scripts: look_at.script
tags: movement
title: Look at

---


This example shows how to rotate a game object to look at the mouse cursor. It reads the mouse position in `on_input` and uses the mathematical function `math.atan2(x, y)` to calculate the angle between the ray to the point to look at and the positive x-axis. This angle is used to set the rotation of the game object to always look at the mouse position. 

The example is suitable for the movement in two dimensions, for platformers or top-down games. For 3D objects, check out the [next example](/examples/movement/look_rotation/).
