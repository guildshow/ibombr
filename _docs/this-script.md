---
title: 03.this函数
permalink: "/docs/this-script/"
note: this函数目前存疑，暂做记录.
redirect_from: "/conduct/index.html"
editable: false
---

## 03. this函数

this函数的使用方法，目前仍然存疑。

基础代码如下：

在下面的示例代码中，TestScript定义了一个虚函数DoSomething，传统的方式，我们可以使用继承重载DoSomething函数实现不同的功能：

````c#
public class TestScript：MonoBehaviour {
void Start () {
	this.DoSomething();
}
    
public virtual void DoSomething()
{
	Debug.Log("DoSomething");
}
````

关于**虚函数**：

>在面向对象程序设计领域，C++、Object Pascal 等语言中有**虚函数**（英语：virtual function）或**虚**方法（英语：virtual method）的概念。 这种**函数**或方法可以被子类继承和覆盖，通常使用动态调度实现。

在下面的示例中，创建了两个类，将这两个类都加载到同一个Game Object上。TestScript函数使用SendMessage函数调用了游戏对象上的DoSomething函数，注意，这个函数是定义在另一个类中，如果需要不同版本的DoSomething函数，只需要创建多个不同版本的DoSomething函数即可。使用这种方式的好处是可以使功能更加模块化。

```  c#
public class TestScript：MonoBehaviour {
    void Start () {
    	this.gameObject.SendMessage("DoSomething");
    }
}

public class DoSomethingScript：MonoBehaviour
{
	public void DoSomething(){
		Debug.Log("DoSomething");
	}
}
```

需要注意的是，SendMessage函数的效率较低，追踪错误也比较困难。在下面的示例中，我们混合了继承和组件的特性，首先创建了一个名为DoSomethingBase的抽象类，DoSomethingScript继承DoSomethingBase，TestScript可以直接引用DoSomethingScript中的DoSomething函数。

```c#
public class TestScript：MonoBehaviour {
void Start () {
// GetComponent获取其他组件
	this.gameObject.GetComponent<DoSomethingBase>().DoSomething();
	}
}

public abstract class DoSomethingBase：MonoBehaviour{
	public abstract void DoSomething();
}

public class DoSomethingScript：DoSomethingBase{
	public override void DoSomething(){
		Debug.Log("DoSomething");
	}
}
```

后续可以在了解更多内容之后，再来研究此函数实质。