---
category: sprite
path: sprite/samplers
layout: example
tags: sprite
title: Multiple Sprite Samplers
brief: This example shows how to sample from more than one image when drawing a sprite
scripts: multi_sample.script, multi_sample_sprite.fp
---

The example uses a sprite with a material with two samplers:

![](multi_sample_sprite_material.png)

The samplers are assigned to two atlases, `one.atlas` and `two.atlas`:

![](multi_sample_collection.png)

Each atlas contains a Defold logo:

![](one_atlas.png)

![](two_atlas.png)

Note the rename pattern in `two.atlas`. The rename pattern is required so that it is possible to sample from the same location in both atlases. 

The color data from the two samplers is mixed/interpolated in the fragment program to produce a final color. The amount of interpolation is controlled in the `mix_amount` fragment constant. The `mix_amount` is animated between 0.0 and 1.0 in the `multi_sample.script`
