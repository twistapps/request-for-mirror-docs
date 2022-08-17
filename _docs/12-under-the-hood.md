---

title: Shortcomings
permalink: /under-the-hood
excerpt: "We've found a workaround."

author_profile: false
author: Twist Apps

---

Due to Mirror's limitations, generic types in *NetworkBehaviour*-derived classes are not supported.
Neither does invoking commands from children work.

So we found a workaround to make this package's existence possible.

## How we hide [Command] implementations and make Mirror support generics

We generate code.

By default, CodeGen module refreshes generated scripts on compilation. This could be changed in settings.

Code generation settings are available at `Tools > TwistApps > CodeGen Settings`