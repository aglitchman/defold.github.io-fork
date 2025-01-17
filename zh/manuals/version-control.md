---
layout: manual
language: zh
github: https://github.com/defold/doc
toc: ["版本控制","Changed files","Git"]
title: 版本控制
brief: 本教程介绍了内置版本控制系统是如何工作的.
---

# 版本控制

Defold 为密切合作的小游戏团队而设计. 团队成员可以并行工作而不必担心融合问题. Defold 使用 [Git](https://git-scm.com) 进行版本控制. Git 有助于分布式团队合作而且为各种工作流提供了得力的工具.

## Changed files

本地项目文件改变时, Defold 在 *Changed Files* 面板中追踪这些改变, 把每个新增, 删除或者修改了的文件罗列出来.

![changed files](/manuals/images/workflow/changed_files.png)

选中一个文件点击 <kbd>Diff</kbd> 来查看更改, 或者点击 <kbd>Revert</kbd> 来把文件还原回上次同步后的状态.

## Git

Git 是知名的版本控制系统. 通过保留差别实现版本控制, 所以即使提交了很多版本其占用空间也不是很大. 但是像图片和声音这样的二进制文件, 就无法从 Git 的存储方案中收益了. 它们每次的提交都会保存整个文件而不是差异. 对于小文件还好办 (JPEG 或者 PNG 图片, OGG 声音文件之类的), 但是对于大型工程源文件 (PSD 文件, Protools 项目文件之类的). 这些文件随着项目进展越长越大. 这样的文件最好别用 Git 托管而是另找地方进行备份.

使用 Git 便于团队合作. 在 Defold 使用团队工作流. 同步时, 流程如下:

1. 各自的本地更改会被储存起来以便同步失败时可以恢复.
2. 服务器上有更新推送.
3. 更新与本地比较, 如果有冲突会提示解决.
4. 可以选择把本地修改推送到服务器.
5. 如果本地与服务器有冲突, 会提示解决.

如果选择使用 Git 命令行或者其他第三方工具进行拉取, 推送, 提交, 混合, 建立分支等等都是可以的.
