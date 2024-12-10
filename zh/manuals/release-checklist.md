---
layout: manual
language: zh
github: https://github.com/defold/doc
toc: ["发布前检查"]
title: 发布前检查
brief: 本教程介绍了发布游戏前应该做的检查事项.
---

# 发布前检查

本教程介绍了发布游戏前应该做的检查事项.

* 屏幕尺寸 - 游戏是否能在比项目设置中的默认宽高更大或者更小的屏幕上适配良好?
  * 此处渲染脚本的 projection 和 gui 里的 layout 起到很大作用.
* 宽高比 - 游戏是否能在与默认宽高比不同的屏幕上适配良好?
  * 此处渲染脚本的 projection 和 gui 里的 layout 起到很大作用.
* 刷新率 - 游戏是否能在比默认 60 Hz 更高刷新率的屏幕上运行?
  * 此处 game.project 中的 Display 部分里的 vsync 和 swap interval 起到很大作用. 


