---
layout: post
title: 02.序列化
categories: [unity notes]
tags: [unity, hello world, study, notes]
description: Unity中的序列化功能.
---

## 02. 序列化

在Unity中，配置一些角色属性数值的时候，可以直接在脚本中暴露出来，在场景中进行配置。以下为示例：

```c#
public class Player：MonoBehaviour {
    public int id = 0;
    public string m_name = "default";
    public float m_speed = 0;
    public Camera m_camera;
    public List<string> items;	
    // ……
```

将这个脚本指定给场景中的任意一个游戏体，然后就可以在`Inspector`窗口中配置`Player`实例的`public`成员变量初始值了，为了显示方便，Unity会在编辑器中自动去掉前缀m_，如下图所示：

![serialization](/images/unity/serialization1.png)

默认只有继承自MonoBehaviour的脚本才能序列化。如果是一个普通的C#类，需要使用添加System.Serializable属性才能序列化，如下所示。

```c#
[System.Serializable]
public class PlayerData
{
    public int id = 0;
    public string m_name = "default";
    public float m_speed = 0;
    public Camera m_camera;
    public List<string> items;
}
public class Player：MonoBehaviour {
	public PlayerData m_data;
}
```

现在，所有的序列化变量都放到了m_data中。

Unity只能序列化public类型的变量，且不能序列化属性。Unity中的很多功能都可以通过序列化在场景中直接编辑，甚至不用编写代码即能实现，优点是节省代码，便于修改，缺点是依赖场景中的设置，比较难以整体控制。