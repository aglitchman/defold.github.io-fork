---
layout: manual
language: zh
github: https://github.com/defold/doc
toc: ["蒙版","创建蒙版节点","裁剪蒙版","蒙版局限性","层"]
title: GUI 蒙版教程
brief: 本教程介绍了创建使用蒙版剪裁遮蔽其他 GUI 节点的方法.
---

# 蒙版

GUI 节点可以作为 *蒙版* 节点---遮蔽影响其他节点的显示方式. 本教程介绍了其用法.

## 创建蒙版节点

方块, 文本 和 饼状图节点可以被裁剪. 要创建裁剪节点, 在 GUI 里添加一个节点, 然后设置相关属性:

Clipping Mode
: 裁剪模式.
  - `None` 不施加裁剪.
  - `Stencil` 施加裁剪.

Clipping Visible
: 选中则蒙版内容可见.

Clipping Inverted
: 选中则遮蔽内容反转.

然后把被裁剪节点作为蒙版子节点加入进来.

![Create clipping](/manuals/images/gui-clipping/create.png)

## 裁剪蒙版

原理上裁剪是把节点写入 *裁剪缓冲区*. 此缓冲区包含蒙版: 就是告诉显卡哪些像素该渲染, 哪些不该渲染.

- 一个没有父蒙版的节点, 如果设置了 clipping mode 为 `Stencil` 的话相当于把它的形状 (或者其反转形状) 写入裁剪蒙版保存在裁剪缓冲区当中.
- 如果一个蒙版节点有父蒙版那么它会继续裁剪父蒙版. 子蒙版不会 _继承_ 当前蒙版, 只会继续剪裁当前蒙版.
- 非蒙版节点作为蒙版的子节点的话, 会被父蒙版层级裁剪渲染.

![Clipping hierarchy](/manuals/images/gui-clipping/setup.png)

这里, 我们建立了节点的三层结构:

- 六边形和矩形都是蒙版节点.
- 六边形是第一个蒙版, 矩形进一步裁剪.
- 园是最下层被裁剪的普通节点.

这种结构下可以有四种裁剪方式. 绿色标志出园被裁剪以后的样子. 结果如下所示:

![Stencil masks](/manuals/images/gui-clipping/modes.png)

## 蒙版局限性

- 蒙版数最大不超过 256 个.
- _蒙版_ 节点最大嵌套8层. (只计算设置了蒙版的节点)
- 同层次蒙版不超过 127 个. 每深一层, 数目减半.
- 反转蒙版很耗性能. 最多8个反转蒙版并且每个反转蒙版会使非反转蒙版的最大数目减半.
- 裁剪渲染基于蒙版节点的 _几何形状_  (而非纹理). 设置 *Inverted clipper* 可以反转蒙版渲染.


## 层

层用于控制节点的渲染顺序 (以及合批顺序). 使用层和蒙版节点时原本的层顺序会被覆盖. 层顺序的优先级高于蒙版顺序---如果一个层的节点与蒙版节点组合在一起, 如果启用蒙版的父节点属于比其子节点更高的层，则裁剪可能会发生乱序. 没被分配层的子节点仍具备父子结构, 继父节点之后还会被渲染和裁剪.

<div class='sidenote' markdown='1'>
蒙版节点及其层级有层设置的话会优先显示, 没有设置的话按照普通顺序显示.
</div>

![Layers and clipping](/manuals/images/gui-clipping/layers.png)

本例中, 节点 "Donut BG" 和 "BG" 都使用了 layer 1. 它们的渲染顺序遵循层级即 "Donut BG" 先于 "BG" 渲染. 然而, 子节点 "Donut Shadow" 归为 layer 2 即更高层级, 则它的渲染晚于这两个节点. 这种情况下, 渲染顺序为:

- Donut BG
- BG
- BG Frame
- Donut Shadow

可见 "Donut Shadow" 对象基于层级被两个蒙版节点裁剪, 即使它是蒙版节点的唯一子节点.
