---
title: Integration
permalink: /integration
excerpt: "How to add integrate 3rd party packages with Modula."

author_profile: false
author: Twist Apps

integr_mirror: common/integrations/mirror.md
---

Modula supports easy integration for any type that extends `MonoBehaviour`.

# Creating custom Module type
To create a new module type, simply add new class and paste the following:

{% highlight C# %}
using System;
using Modula;
using Modula.Optimization;
using UnityEngine;


public abstract class YourModule : CustomBehaviour, IModule
{
    public TimingConstraints UpdateInvocationConstraints => DefaultImplementation.UpdateConstraints;
    public virtual TypeList RequiredOtherModules { get; } = TypeList.None;

    private ModuleDefaultImplementation _defaultImplementation;
    // ReSharper disable once MemberCanBePrivate.Global
    protected ModuleDefaultImplementation DefaultImplementation
    {
        get { return _defaultImplementation ??= new ModuleDefaultImplementation(this); }
    }

    public ModularBehaviour Main => DefaultImplementation.Main;

    public void OnAdd()
    {
        DefaultImplementation.OnAdd();
    }

    public void AddModule(Type moduleType)
    {
        DefaultImplementation.AddModule(moduleType);
    }

    public string GetName()
    {
        return DefaultImplementation.GetName();
    }

    public DataLayer GetData()
    {
        return DefaultImplementation.GetData();
    }

    public virtual void ModuleUpdate()
    {
    }

    public virtual void Update()
    {
        DefaultImplementation.Update();
    }
}{% endhighlight %}

- Replace `"YourModule"` with your preferred name
- Replace `"CustomBehaviour"` with any other class that extends MonoBehaviour

Now you can use **YourModule** class in the same way you use `Module`, but it also supports
all the features implemented in **CustomBehaviour**!
{: .notice--success}


# Built-In integrations
These are integrations with 3rd party packages that are supported out-of-the-box: 

## Mirror
{% if page.integr_mirror %}
  {% include_relative {{ page.integr_mirror }} %}
{% endif %}