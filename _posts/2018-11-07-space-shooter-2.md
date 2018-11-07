---
layout: post
title: "07.太空射击游戏开发02"
description: 第2章，从头开始制作一款简单的太空射击游戏之2。
category: unity notes
tags: unity, hello world, study, notes
---

太空射击游戏的第二部分，创建一个角色，并使其拥有以下能力：

* 操控移动
* 配置速度参数

以下为流程：

### 1.创建主角

1.1 将`Prefab`预置体`Player.fbx`拖入`Hierarchy`窗口，创建主角飞船的游戏体；此时在`Scene`窗口中能够找到`Player`对应的实例；

1.2 调整游戏体`Player`的角度，在`Inspector`窗口将其在Y轴旋转180度；如下图：

![Rotation](/images/unity/playerRotation.png)

### 2.基础脚本

2.1 为游戏体`Player`编写脚本；在`Project`窗口下指定文件夹中，使用`Create → C# Script`来创建一个C#脚本，并将其命名为`Player`；

2.2 双击脚本`Player.cs`将其打开，Unity会自动添加基本代码，示意如下：

```C#
using System.Collections;
using UnityEngine;

public class Player : MonoBehaviour {

	// Use this for initialization
	void Start () {
		
	}
	
	// Update is called once per frame
	void Update () {
		
	}	
}
```

其中，`Player`是类的名字，这个名字需与当前脚本的文件名一致；默认继承自`MonoBehaviour`，只有继承自`MonoBehaviour`的类，才能作为Unity的**脚本组件**使用；

2.3 将2.2步所写的脚本，指定给游戏体`Player`使用；方法是拖动到其`Inspector`窗口中；

2.4 可以自定义所创建的脚本，出现在菜单栏`Component`中的位置；默认是`Component → Script`下面，修改时在脚本的`Player`类之前添加`AddComponentMenu`属性，如下：

```c#
[AddComponentMenu("MyGame/Player")]
public class Player : MonoBehaviour
```

此时`Player`脚本将会出现在`Component → MyGame`之下，如下图：

![自定义脚本位置](/images/unity/resetScriptSeat.png)

### 3.控制移动

继续增加脚本内容，使其可以控制游戏体`Player`移动；代码示意如下：

```c#
//以上内容省略...
public class Player : MonoBehaviour {
	public float m_speed = 1;
    void Start () {		
	}
	
	// Update is called once per frame
	void Update () {
		float movev = 0;
		float moveh = 0;

		if (Input.GetKey(KeyCode.UpArrow)){
			movev -= m_speed * Time.deltaTime;
		}

		if (Input.GetKey(KeyCode.DownArrow)){
			movev += m_speed * Time.deltaTime;
		}

		if (Input.GetKey(KeyCode.LeftArrow)){
			moveh += m_speed * Time.deltaTime;
		}

		if (Input.GetKey(KeyCode.RightArrow)){
			moveh -= m_speed * Time.deltaTime;
		}

		//move
		this.transform.Translate(new Vector3(moveh,0,movev));
    }
}
```

说明如下：

3.1 `Input`是一个包装了输入功能的类，它包括几乎所有的键盘、鼠标或触控操作函数。

3.2 `Time.deltaTime`表示每帧的经过时间，那些需要每帧做增减变动的数值都建议乘上`Time.deltaTime`。在本示例中，速度与`Time.deltaTime`相乘，表示每帧移动N米距离。

3.3 `this.transform`调用的是游戏体的`Transform`组件，`Transform`组件提供的主要功能都是和移动、旋转、缩放游戏体有关的。我们调用了`Translate`函数移动游戏体，其中有一个`Vector3`类型的参数，用来表示x、y、z三个方向上的移动距离。

3.4 效率优化，在对象初始化时调用`this.transform`组件，并将其保存；最后再于`Update`函数中，调用保存的函数，而非`this.transform`组件；示意如下：

```c#
//上略...
public class Player : MonoBehaviour {
	//其他略...
    protected Transform m_transform;
    void Start () {
            m_transform = this.transform;
        }
    void Update () {
        //其他略...
        //move
            this.m_transform.Translate(new Vector3(moveh,0,movev));
    }
}
```

在Update函数中修改控制移动的代码，将`this.transform`替换为`this.m_transform`，这样程序就不用每帧都去查找`Transform`组件，提高了程序的运行效率。

3.5 配置速度。选择主角飞船游戏体`Player`，在`Inspector`窗口中找到`Player`脚本组件，将`Speed`的值加大至6；如下图：

![修改Speed参数数值](/images/unity/PlayerSpeedInsp.png)

`Speed`的值与`Player`脚本内的`m_speed`的值是对应的，这样只需要在场景中修改`Speed`的值就可以改变飞船的移动速度，而不用每次都去修改原始的代码。

