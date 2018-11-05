---
layout: post
title: "05.预置体Prefab"
description: Prefab是Unity开发中的重要元素，主要用于Game Object的设置重用。
category: unity notes
tags: unity, hello world, study, notes
---

Prefab又称`预置体`，是Unity开发中的重要元素。因为Unity中的Game Object作为游戏中的基本元素是没有功能的，所以通常需要给Game Object添加各种组件，如脚本、物理碰撞或动画控制器等，当添加了这些组件后，可能还需要对组件的参数进行设置，但是如何重用这些设置呢？这时就要用到Prefab，我们可以将在场景中编辑的Game Object制作成一个Prefab保存在工程中，这样就可以随时拿来重用了。

创建Prefab非常简单，当在场景中完成对Game Object的配置后，只要将其拖动到Project窗口中（Assets）即创建了Prefab，如下图所示。这时Project窗口中的Prefab与场景中的实例是相关联的。

![prefab](/images/unity/prefab1.png)

对于Prefab有以下规则：

1. 删除场景中的实例不会影响到Project窗口中的Prefab。
2. 如果修改了场景中的实例，选择Inspector窗口右上角的`Prefab->Apply`，Project窗口中保存的Prefab则会自动同步到该修改结果。
3. 如果修改了场景中的实例，选择Inspector窗口右上角的Prefab->Revert，则会返回到Prefab的设置。
4. 如果修改了Prefab的某项设置，场景中的实例又没有修改过该项设置，场景中的实例则会自动同步到与Prefab相同的设置。

此部分内容较为简单，不赘述。