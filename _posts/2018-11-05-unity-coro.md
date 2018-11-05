---
layout: post
title: "04.Unity协程编程"
description: Unity中类似多线程处理的一种方式.
category: unity notes
tags: unity, hello world, study, notes
---

在游戏的逻辑中，经常会遇到先完成某个任务，等待一定时间后，再去做某个任务，又或者在提交一个请求后，需要等待请求返回结果再执行后面的代码。Unity提供了一种称为协程的编程方式，它允许在不堵塞主线程的情况下，在协程函数中堵塞或循环，听起来有些类似多线程，但注意协程不是多线程，只是方便了程序编写。

协程函数需要使用关键字`IEnumerator`定义，并一定要使用关键字`yield`返回。协程函数不能直接调用，需要使用函数`StartCoroutine`将协程函数作为参数传入，下面是一段示例代码：

```C#
using System.Collections; // 使用协程需要这个名称域
using UnityEngine;

public class CoroTest：MonoBehaviour // 协程必须运行在MonoBehaviour对象中
{
	void Start () {
		Coroutine coro = StartCoroutine(DoSomethingDelay(1.5f)); // 必须使用StartCoroutine执行协程
		// Destroy(this.gameObject); 如果删除了当前游戏体，协程也会随着消失
		// StopAllCoroutines(); // 停止所有运行于当前MonoBehaviour的协程
		// StopCoroutine(coro); // 停止指定的协程
		StartCoroutine(RunLoop());
	}
	// 定义协程的函数体
	IEnumerator DoSomethingDelay(float sec){
      	yield return new WaitForSeconds(sec); // 等待
		Debug.Log("运行");
		//if () 
        // yield break; // 满足条件中断协程
        // yield return new WaitForSeconds(sec); // 可以多次等待
        //StartCoroutine(DoSomethingDelay(1.5f)); // 可以一直循环执行下去
        }
    IEnumerator RunLoop(){ // 在协程中创建循环
    	while (true){ // 可以在循环中设置中断条件
            Debug.Log("循环中");
            yield return 0; // 没有等待，立即返回
        }
    }
}
```

此部分内容较为复杂，待以后再行细读了解。