---
title: Timing Constraints
permalink: /timing-constraints
excerpt: "How to take off fast!"

author_profile: false
author: Twist Apps
---

This feature is firstly added for _optimization purposes_, but there are even more use cases for that.

## Technical Details
`TimingConstraints()` class accepts `Action` argument in constructor.
Then you can use `TimingConstraints.SetFrames` or `TimingConstraints.SetSeconds` to determine,
how often that action should be called.

In practice, this means you can make your own version of the `Update()` function,
but also constrain it to be called, for example, once every 10 frames only.

If you have some heavy logic inside Update(), using TimingConstraints to improve performance is a good option.

## Code Example

    {% highlight C# %}// Example TimingConstraints usage
    public class Example : MonoBehaviour
    {
        private var _timingConstraints 
            = new TimingConstraints(Foo).SetSeconds(.1f);
        
        private void Update() {
            _timingConstraints.Update(time.deltaTime);
        }
        
        private void Foo() {
            /// Some very heavy code
            ...
        }
    }{% endhighlight %}
    
**Notice:** deltaTime argument is optional so you can experiment with time.
{: .notice}

In this example method Foo() will be called roughly 10 times per second.
As you can see, TimingConstraints instance expects that you will call its inner Update function every frame.


## Usage in modules
TimingConstraints() is supported by any `Module` by default.

In modules, an instance of `TimingConstraints()` is used to control the invocation frequency of `ModuleUpdate()` method.
You can change constraints' settings by accessing `UpdateInvocationConstraints` field.

- use `UpdateInvocationConstraints.SetFrames(frames)` to restrict how often `ModuleUpdate` is being called, in frames
- use `UpdateInvocationConstraints.SetSeconds(seconds)` - same as the above but in seconds

For example, you can constrain ModuleUpdate() to be called every 5th frame only, 
or every 1/10 of a second.