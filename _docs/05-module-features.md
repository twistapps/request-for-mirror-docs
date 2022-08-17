---
title: Module Features
permalink: /module-features
excerpt: "How to take off fast!"

author_profile: false
author: Twist Apps
---

#### `Main `

**Description**: refers to the [`ModularBehaviour`](/behaviour-features) that this module is attached to.
{: .notice--info}

{% highlight C# %}//Example
public void Awake()
{
    ModularBehaviour main = this.Main;
}{% endhighlight %}

#### `RequiredOtherModules`

**Description**: add types to this `TypeList` to specify which other modules
are required and therefore should be added to the [Main](#main) gameObject
after you add this module.
{: .notice--info}

{% highlight C# %}//Usage
public override TypeList RequiredOtherModules { get; }{% endhighlight %}

{% highlight C# %}//Example
public override TypeList RequiredOtherModules { get; } 
    = new TypeList()
    .Add(typeof(SecondModule))
    .Add(typeof(ThirdModule));{% endhighlight %}

#### `UpdateInvocationConstraints`

**Description**: refer to this property to change how often `ModuleUpdate()` should be called
{: .notice--info}

{% highlight C# %}//Usage
UpdateInvocationConstraints.SetFrames(frames);
UpdateInvocationConstraints.SetSeconds(seconds);{% endhighlight %}

{% highlight C# %}//Example
public void Awake()
{
    UpdateInvocationConstraints.SetFrames(15);
    UpdateInvocationConstraints.SetSeconds(3.5f);
}{% endhighlight %}

{% highlight C# %}{% endhighlight %}