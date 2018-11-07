---
layout: post
title: "08.太空射击游戏开发03"
description: 第2章，从头开始制作一款简单的太空射击游戏之3。
category: unity notes
tags: unity, hello world, study, notes
---

太空射击游戏的第3部分，创建一个子弹，然后让主角飞机能够发射子弹；以下为流程：

### 1.创建子弹

1.1 将子弹的模型文件`rocket.fbx`拖动到`Hierarchy`窗口，创建子弹的游戏体`Rocket`；

1.2 创建脚本文件`Rocket.cs`，并指定给子弹的游戏体`Rocket`，作为组件；

1.3 编辑`Rocket.cs`脚本，如下：

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[AddComponentMenu("MyGame/Rocket")]
public class Rocket : MonoBehaviour {

	public float m_speed = 10;
	public float m_liveTime = 1;
	public float m_power = 1.0f;
	protected Transform m_transform;
	// Use this for initialization
	void Start () {
		m_transform = this.transform;
		Destroy(this.gameObject,m_liveTime); //延迟一段时间后摧毁自己
	}
	
	// Update is called once per frame
	void Update () {
		m_transform.Translate(new Vector3(0,0,-m_speed * Time.deltaTime));
	}
}

```

在上述脚本中，我们用`m_speed`、`m_liveTime`、`m_power`来控制子弹的速度、生存时间和威力属性；用`m_transform`保存了组件`this.transform`，并通过`Update`函数中的`m_transform.Translate`来使子弹移动；这部分同飞船移动类似，都是调用了`Transform`组件的功能。

1.4 此时运行游戏，`Scene`中的子弹`Rocket`将自动往前飞行，一段时间后消失；

### 2.创建子弹预置体

我们需要通过操作飞船来发射子弹，所以需要将子弹设置为预置体；

2.1 拖动`Hierarchy`中的子弹游戏体`Rocket`，至`Project`窗口中空白处，即可创建子弹的预置体Prefab；如下图：

![Rocket预置体](/images/unity/rocketPrefab.png)

2.2 此时`Hierarchy`中的游戏体`Rocket`就没用了，删除即可；

### 3.发射子弹

此时需要调整飞船游戏体`Player`的脚本。

3.1 在`Player.cs`脚本中，添加一个`Transform`属性，指向子弹的Prefab，即：

```c#
public Transform m_rocket;
```

随后将子弹的预置体Prefab，拖动至`Player`的`Inspector`窗口中`rocket`属性中，如下图：

![transformRocket](/images/unity/transformRocket.png)

3.2 再修改`Player.cs`脚本，增加如下内容：

```c#
void Update () {
    //....
    //按空格键或鼠标左键发射子弹
	if (Input.GetKey(KeyCode.Space)||Input.GetMouseButton(0)){
				Instantiate(m_rocket,m_transform.position,m_transform.rotation);
    }
}
```

Unity的游戏体只能使用Instantiate函数实例化，不能使用new。

### 4.调整发射频率

按上述配置，按空格时游戏每帧都会创建一个`Rocket`的实例；我们需要控制发射子弹的速度（频率）；

4.1 增加发射计时，如下：

```c#
//...
float m_rocketTimer = 0;
```

4.2 在按空格前判断当前计时

```c#
//...
void Update () {
	//...
    m_rocketTimer -= Time.deltaTime;
		if (m_rocketTimer <= 0){
			m_rocketTimer = 0.1f;
			if (Input.GetKey(KeyCode.Space)||Input.GetMouseButton(0)){
				Instantiate(m_rocket,m_transform.position,m_transform.rotation);
			}		
		}
}
```

4.3 此时运行游戏，按空格时，每0.1秒发射1颗子弹；