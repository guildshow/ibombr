---
layout: post
title: "06.太空射击游戏开发01"
description: 第2章，从头开始制作一款简单的太空射击游戏。
category: unity notes
tags: unity, hello world, study, notes
---

整理提纲。这一部分，主要是环境相关内容的创建和设置；

基础流程说明如下：

### 1.创建场景

1.1 用菜单栏的`File → New Scene`创建一个新的场景；

1.2 用菜单栏的`File → Save Scene As`保存该场景；

### 2.创建背景

2.1 用菜单栏的`GameObject → 3D Object→Plane`创建一个平面`Mars`，作为背景；

2.2 在`Project`窗口中`Create → Material`创建一个材质球`MarsBG`；材质球可以在后续工作中，应用到场景物件材质；

2.3 将刚刚创建的材质球，`MarsBG`的贴图指定为`mars.png`；方法可以是选择`MarsBG`之后，拖动`mars.png`至材质球`MarsBG`的`Inspector`窗口的`Albedo`上面；如下图：

![serialization](/images/unity/albedo.png)

2.4 在`Scene`窗口中选择2.1步中创建的`Plane`平面`Mars`，然后将2.2中创建的材质球拖动至其上。此时`Mars`平面的`Inspector`窗口中，`Materials`的`Element0`应为材质球的名字；如下图：

![serialization](/images/unity/marsBGinspector.png)

2.5 我们要把2.1步中创建的`Plane`平面`Mars`调整为与材质球`MarsBG`的贴图`mars.png`相匹配的球形；选择`Plane`平面，在`Inspector`窗口中将`Rendering Mode`设为`Cutout`，即可以显示出相应的效果；

### 3.制作星空

3.1 再创建一个`Plane`，使其置于背景`Mars`的下方；命名为`SpaceBG`；

3.2 为其创建一个材质球，命名为`starBG`；指定其贴图为`star.png`；

3.3 该背景图不需要接收光线，我们将其材质球`starBG`的`Shader`属性调整为`Unlit/Texture`；

3.4 将材质球`starBG`指定给星空背景`SpaceBG`；

### 4.星空动画

为第3步所制作的星空，制作动画；

4.1 在`Project`窗口创建`Animator Controller`，随后拖动到星空背景`SpaceBG`的`Inspector`窗口中作为其组件；

4.2 打开动画窗口，路径是菜单栏的`Window → Animation → Animation`，在保持`SpaceBG`选中的前提下，点击`Animation`窗口中的`Create`来创建一个新的动画文件；

4.3 在保持`SpaceBG`选中的前提下，点击`Animation`窗口中的`Add Property`按钮，增加一个动画UV属性；随后选择`Material._Main_Tex_ST`，这是用来控制材质球的偏移的；

4.4 单击左上角的`动画记录`按钮进入动画录制状态，将时间轴前进至`30帧`左右，将`Material._Main_Tex_S`属性中的`w`值设为-1，播放动画，星空贴图将会缓缓移动。注意，此处我实际操作时，是将其跳至`1800帧`，即`30秒`左右，再修改动画记录值的；

![serialization](/images/unity/spacebgAnimation.png)

默认动画是循环播放的，选择动画文件，在Inspector窗口中设置它的Loop Time，即可改变循环模式；

### 5.配置摄像机

5.1 在`Scene`窗口中，按住`Alt`后用鼠标左键调整角度；

5.2 在`Hierarchy`窗口中选中`Main Camera`，然后在菜单栏中，选择`GameObject → Align With View`，使摄像机视角与当前视图一致；

`Hierarchy`窗口是一个名称列表，并可以按子父层级关系排列显示，它们与`Scene`窗口中出现的游戏体是一一对应的。

### 6.调整灯光

6.1 在`Window → Rendering → Lighting Settings`中设置灯光；在`Environment Lighting`属性中设置环境光；按书中需求，将`Source`由`Skybox`改为`Color`，然后调整`Ambient Color`颜色；

6.2 因为本示例不需要使用`Lightmap`，取消`Lighting`界面中的`Auto Generate`选项，以防止Unity自动为场景构建`Lightmap`；如下图：

![serialization](/images/unity/lightingsetting.png)

6.3 创建一个点光源，方法是菜单栏`GameObject → Light → Point Light`，并调整其位置，使其位于火星背景`Mars`的上方；然后通过调节其`Range`属性，改变其照亮范围；调节`Intensity`属性，改变其亮度；