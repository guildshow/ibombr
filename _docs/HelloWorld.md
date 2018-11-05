---
title: 01.hello world
permalink: "/docs/HelloWorld/"
note: 在Unity中编写Hello World出现的错误.
redirect_from: "/conduct/index.html"
editable: false
---

## 01. Hello World

开始学习Unity引擎相关的东西。

在使用`C#`编写`Hello World`的内容时，犯了一个小错误，导致半天没有在游戏中显示 Hello World 的文本内容，并且查了半天错误都没有找到问题所在。

流程如下：

1. 编写一个HelloWorld的C#脚本；
2. 拖动到MainCamera上，作为其组件；
3. 开始游戏；

而这个HelloWorld的脚本内容如下：

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class HelloWorld : MonoBehaviour {

	// Use this for initialization
	void Start () {
		
	}
	
	// Update is called once per frame
	void Update () {
		
	}
	
	void onGUI () {
		//改变字体大小  
        GUI.skin.label.fontSize = 120;
        //定位显示(左边距x, 上边距y, 宽, 高)  
        GUI.Label(new Rect(10, 50, 900, 120), "Hello World!");

	}
}

```

最后发现问题出在`onGUI`之上，其应为`OnGUI`；

一个简单的大小写错误，导致Unity未识别onGUI方法，而未运行后续的内容。

最后使用了

```C#
Debug.LogError("someting");
```

方法才找到问题所在。

此为备忘警示。