---
layout: manual
language: zh
github: https://github.com/defold/doc
toc: ["导入2D图像","创建 Defold 资源","使用 Defold 资源"]
title: 导入和使用2D图像
brief: 本教程介绍了如何导入和使用2D图像.
---

# 导入2D图像

Defold 支持2D游戏常见的可视内容. 可以使用 Defold 制作静态或动态Sprite, UI 组件, 粒子特效, 瓷砖地图 和 位图字体. 先导入图片文件再创建相应资源以使用它们. 把文件系统任意图片文件拖放到 Defold 编辑器的 *资源面板* 中即完成导入操作.

![Importing files](/manuals/images/graphics/import.png)

<div class='sidenote' markdown='1'>
Defold 支持 PNG 和 JPEG 图片格式. 其他格式要先转换成支持格式后使用.
</div>


## 创建 Defold 资源

图片导入 Defold 后即可创建相应资源:

![atlas](/manuals/images/icons/atlas.png) Atlas
: 图集是多张图片组成的大图. 图集可以包含单个图片或者 *动画组*, 即组成逐帧动画的一组图片.

  ![atlas](/manuals/images/graphics/atlas.png)

关于图集资源详情请见 [图集教程](/zh/manuals/atlas).

![tile source](/manuals/images/icons/tilesource.png) Tile Source
: 瓷砖图集是由小图按一定顺序排列好的大图. 这种图又被叫做 _精灵表_. 瓷砖图集也可以通过指定第一帧与最后一帧的图块, 来创造逐帧动画. 也可以使用图片自动生成图块的碰撞方块.

  ![tile source](/manuals/images/graphics/tilesource.png)

关于瓷砖图集资源详情请见 [瓷砖图集教程](/zh/manuals/tilesource).

![bitmap font](/manuals/images/icons/font.png) Bitmap Font
: 位图字体是 PNG 图片格式的文字表. 这种字体比起 TrueType 或者 OpenType 字体文件并没有性能优势, 但是由于是图片, 颜色阴影等效果可以随意加入.

关于字体资源详情请见 [字体教程](/zh/manuals/font/#位图 BMFont).

  ![BMfont](/manuals/images/font/bm_font.png)


## 使用 Defold 资源

当图片转化为图集或者瓷砖图集之后就可以用于各种可视组件之中:

![sprite](/manuals/images/icons/sprite.png)
: Sprite是可以显示的图片或者逐帧动画.

  ![sprite](/manuals/images/graphics/sprite.png)

关于Sprite详情请见 [Sprite教程](/zh/manuals/sprite).

![tile map](/manuals/images/icons/tilemap.png) Tile map
: 瓷砖地图是由若干源自瓷砖图集的地图块 (图片连同其碰撞方块) 组成的可视组件. 瓷砖地图不能使用图集资源.

  ![tilemap](/manuals/images/graphics/tilemap.png)

关于瓷砖地图详情请见 [瓷砖地图教程](/zh/manuals/tilemap).

![particle effect](/manuals/images/icons/particlefx.png) Particle fx
: 粒子是由粒子发射器发射的, 源自图集或者瓷砖图集图片生成的一组组静态图片或逐帧动画.

  ![particles](/manuals/images/graphics/particles.png)

关于粒子特效详情请见 [粒子特效教程](/zh/manuals/particlefx).

![gui](/manuals/images/icons/gui.png) GUI
: GUI 方块节点和 饼图节点也可以使用来自图集或者瓷砖图集的静态或逐帧动画.

  ![gui](/manuals/images/graphics/gui.png)

关于GUI详情请见 [GUI教程](/zh/manuals/gui).
