---

title: Other Assets by Me
permalink: /other-assets
excerpt: "Other assets I made."

author_profile: true
author: Twist Apps

---

All of my opensource projects for Unity could be found at [TwistApps](https://github.com/twistapps), 
the GitHub organization dedicated to these.

Sneak Peek on what you could find there:
# [Modula](http://modula.twistapps.com)
Modula is a tool which makes you write code faster and cleaner.
Split your codebase into small independent modules and re-unite (rebuild them together) them again with ModularBehaviours,
or make templates to define interchangeable groups of modules so they are easily swapped around in editor, or in runtime.

## Most important definitions
**Module** is a logically independent part of code which you write. <br />
**ModularBehaviour** is the same as MonoBehaviour but it is used as a soft dependency system for a predefined set of modules.
This means each module is optional and you could add/remove it on runtime.<br />
**Basepart** is a set of *interchangeable* modules. That means you should pick one at a time and it will replace another. For example, if you have multiple camera control modes,
but there's only one active at a time, these could make a basepart!<br />
**Template** is just `ModularBehavour` that is levelled up! Templates are made of baseparts instead of pure modules.