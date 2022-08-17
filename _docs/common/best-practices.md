
## Best Practices

#### Modules

##### Require any other module(s)
If your module requires other module(s) to work properly,
just set the `RequiredOtherModules` property as in the example:

    {% highlight C# %}public class WithDependencies : Module {
        public override TypeList RequiredOtherModules { get; } 
        = new TypeList()
            .Add(typeof(ModuleFoo))
            .Add(typeof(ModuleBar));
    }{% endhighlight %}

##### Require any unity Component 
If your module requires some unity Component(s) to work properly,
just use the `RequireComponent()` attribute:

    {% highlight C# %}[RequireComponent(typeof(Rigidbody))]
    public class BallPhysics : Module {
        ...
    }{% endhighlight %}