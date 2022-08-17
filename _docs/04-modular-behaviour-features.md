---
title: Modular Behaviour Features
permalink: /behaviour-features
excerpt: "How to take off fast!"

author_profile: false
author: Twist Apps
---

#### `AvailableModules`

**Description**: add types to this `TypeList` to specify modules that could be connected
to the behaviour.
{: .notice--info}

{% highlight C# %}//Usage
public override TypeList AvailableModules { get; }{% endhighlight %}

{% highlight C# %}//Example
public override TypeList AvailableModules { get; } = new TypeList()
    .Add(typeof(FirstModule))
    .Add(typeof(SecondModule))
    .Add(typeof(ThirdModule));{% endhighlight %}

#### `GetModule`

**Description**: get module of type T (T : IModule)
{: .notice--info}

{% highlight C# %}//Usage
GetModule<T>(){% endhighlight %}

{% highlight C# %}//Example
ModuleFoo module = GetModule<ModuleFoo>();{% endhighlight %}