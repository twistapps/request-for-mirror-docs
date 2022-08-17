---
title: "Overview"
permalink: /uwu
excerpt: "Modula package brings the concept of Modular Entities into Unity Engine."

author_profile: true
author: Twist Apps
---

Modula is a package for Unity Engine that brings in the concept of **Modular Entities**.

---
![logo](https://user-images.githubusercontent.com/26601205/157171576-6774cfdf-e63d-484e-a954-60717e3eb3ad.png)

---

When needed, inherit from `ModularBehaviour` instead of Unity's default `MonoBehaviour` class.
This lets you **split** all the logic inside your behaviour and **move** it into independent modules, which could later be connected to/removed from each instance of that behaviour, using the inspector GUI:

![modula2](https://user-images.githubusercontent.com/26601205/157162945-b4b174e2-c7ce-4d8c-af3d-d07a0f27f20b.gif)

That way by splitting the code into small self-containing modules you could make the codebase cleaner and easier to understand.

# Setup
`work in progress`

## Creating Modules
To create a basic module, simply derive from `Module` class. As we imagine, a module should represent a relatively small self-contained part of your bigger entity/behaviour, such as:
- Engine/Transmission of a car
- Camera setup for the player
- Shooting logic for guns in your awesome FPS ;)
### Example Usage
_Imagine,_ you have the same setup for human characters that could run around a level in your game. The only difference is - most of them are controlled by AI and the last one is the player. By properly issuing the approach Modula offers you, changing that little part of how each 'human' is controlled should be straightforward :).

### Notice from the creator
> I hope Modula helps you to shift away from non-indicative naming e.g. using Controllers, Managers, Getters and Setters for everything. Of course I didn't bring anything exactly new to this world by publishing this package, but I hope that the vision it spreads will actually help you handle the frustration of managing the architecture of each system in your game. As any engineering pattern Modula has its shortcomings, but I believe it should be useful for SOME cases :)

The main purpose of _Modula_ is to nudge **you** to make better systems that consist of self-contained and re-usable parts.

## What is Modula?
Modula provides some base classes which you could derive from instead of `MonoBehaviour`,
so you can take advantage of _modular approach_ as we see it.
Also provides you with some useful hacks, optimization features and, whatever.

### Backstory
For a long time I tried to find a multipurpose solution/framework to make my codebase 
**divided** (therefore, less coupled) as much as possible.
But there was nothing that could exactly fit the vision. 
So lately I came up with the concept of `"modular entities"` and made 
a simple framework based on that idea.

Fairly the idea's not entirely fresh and new, but I tried to find 
a new perspective on the concept to solve common engineering bottlenecks in Unity.

### How to use, step-by-step
- make your first `ModularBehaviour` and take advantage of `Modules`.

Just derive from `ModularBehaviour` instead of `MonoBehaviour`:
    
    public class Car : ModularBehaviour
    {
         ...
         
         // Your code as you always do it
         
         ...
    }

- create some `Modules` which could implement different independent systems for your behaviour.


     public class Engine : Module 
     {
         void Start() { ... }
         
         ...
     }

- get back to yor behaviour and add support of these modules:


    public class Car : ModularBehaviour
    {
          public override TypeList AvailableModules { get; } = new TypeList()
             .Add(typeof(Engine));
         
         // Your code as you always do it
         
         ...
    }

- use custom editor for any new `Car` you create to choose which modules that instance of a car supports:
![image](~/resources/ModuleDependencies.png)

### The problem
Imagine you have `MonoBehaviour` that represents a car 
which could accelerate and break, switch gears and turn.

So if you don't want all the code for these features to be contained 
in a single **Car** class, you need a way to split it up into `'modules'`:
- Engine
- Transmission
- Steering wheel

..and then make **Car** to reference and combine these modules.

> Of course there are many ways to do this, heard of programming patterns? 
> 
>**But** we decided to publish Modula because we believe:
> some people will love our approach <3

### The Solution
 Modula implements new `ModularBehaviour` class which extends `MonoBehaviour`,
 so you can derive from it to make a new entity with support of _modular structure_:
 
     public class Car : ModularBehaviour
     {
         public override TypeList AvailableModules { get; } = new TypeList()
            .Add(typeof(Engine));
         
         
         void Start() { ... }
         
         ...
     }
[AvailableModules] property allows you to declare which modules are supported by this behaviour.
By design it means these modules can be attached to `GameObject` with that behaviour, but **aren't required**.
 
 There's also a new base class called `Module` which you derive from 
 when making new modules:
     
     public class Engine : Module 
     {
         void Start() { ... }
         
         ...
     }
     
Yeah, it's that simple! Now you have an **Engine** that can (but is not required to) be attached to a **Car**.


#### Important to note, that
the implementation above is a _bare minimum_ to make your first ModularBehaviour, but there are a lot more features to enjoy:
- [Requiring other modules for module]
- [ModuleUpdate() is like an optimized Update()]
- [Make handy serializable properties with DataLayers]

#### For those who like promotional texts
Modula brings flexibility into your workflow, nudging you to better isolate each part of your codebase.
If you ever wanted to split up **that large class** which implements every feature of your over-engineered first person controller, Modula could be the solution.

#### Declarative naming

Modula is not only a framework, it's a set of recommendations if you wish that makes you more productive and creative, [because].

#### Now actually, a boring technical explanation
After [setting up modula](installation.md) you now have a new base class to derive from, called ModularBehaviour.
It extends MonoBehaviour, that means you could still use `Awake()`, `Start()`, `Update()`, etc.

    public class FirstModule : Module
    {
        public override BehaviourConstraints RequiredOtherModules { get; } = new BehaviourConstraints()
            .SetConstraints(
                typeof(SecondModule),
                typeof(ThirdModule)
                );
    
        public override void Awake()
        {
            base.Awake();
            UpdateInvocationConstraints.SetFrames(15);
            UpdateInvocationConstraints.SetSeconds(3.5f);
        }
    
    
        public override void ModuleUpdate()
        {
            base.ModuleUpdate();
        }
    }


### Denial of responsibility
Currently this is an early stage of the project, so there's no LTS version or whatever, so I encourage you to use it
only if you're ready to wait a couple of months so Modula gets into its better shape and really begins to shine.
OR if you wanna help developing it, I would be happy seeing any [issues] you publish or pull requests.
See [contribution guidelines](contribution-guide.md) then, I guess. :)