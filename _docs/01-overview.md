---

title: What is Request?
permalink: /
excerpt: "Modula package brings the concept of Modular Entities into Unity Engine."

author_profile: true
author: Twist Apps

install_instructions: common/installation/recommended.md

---

{{site.data.package.displayname}} is a package that extends functionality of [Mirror Networking](https://mirror-networking.com/) for [Unity Engine](https://unity.com), allowing you to define http-like requests
with automatic callbacks on response.
[Get Started](#installation){: .btn .btn--primary .btn--primary .btn--info}

---
![logo](/assets/img/request-banner2.jpg)

---

Currently there are types of requests: `Fetch<TRequest>` and `Post<TRequest,TResponse>`.
Think of these as if you were making a web request: Fetch comes with no request body and Post should have some data sent to the server.

![modula2](https://user-images.githubusercontent.com/26601205/157162945-b4b174e2-c7ce-4d8c-af3d-d07a0f27f20b.gif)

That way by distributing the code into small self-containing modules you could make the codebase cleaner and easier to understand.

## How this Works
Under the hood this package just uses Mirror's high level `[Command]`'s and `[TargetRPC]` calls to exchange data between server and client.

### What's wrong with default Mirror workflow?
If there's some data you need to get from a server, but you don't want to repeatedly synchronize it with [SyncVar]s (don't want to have 'fair play' issues
or that data is rarely needed), there are two possible solutions:
- [Interest Management](https://mirror-networking.gitbook.io/docs/interest-management/custom) - this is too complex for simple things
- *Making a pair of Command and a RPC call to send data then receive a response* - this becomes messy if you have a lot of requests to handle,
mindfully naming each method and making sure to always call TargetSomething in the end of your command - this is just exhausting. Resulting method pairs still look too decoupled after all.
- *Using lower level Network Messages* - but we want something **dead simple**, right?

### Creating a request with this package

To define a new request type, just create a new class and derive it from **Fetch** or **Post**
{% highlight C# %}// Without request body, just fetching a response
public class Req_Example : Fetch<string>
{
    //called on CLIENT
    private void OnConnectedToServer()
    {
        Send(response => Debug.Log(response),
        error => Debug.LogError("Something went wrong: " + error));
    }
    //called on SERVER
    protected override void OnRequest(out RequestStatus status)
    {
        res.SetResponse("Hello World!");
        status = OK;
    }
}{% endhighlight %}

Don't be overwhelmed! The only thing that is actually required to handle the request on server is the OnRequest function.
The OnConnectedToServer method is just how we send the request from client right after it connects to a server.

Let's break down this example:

{% highlight C# %}public class Req_Example ...{% endhighlight %}

- We name this class with `Req_` prefix so it will be highly distinguishable from regular classes. 
That underscore usage is unconventional naming so it's up to you whether you would use it.

{% highlight C# %}... : Fetch<string>{% endhighlight %}

- We derive from Fetch class and set a **response** type for this particular request as `string` using angle brackets.
  
{% highlight C# %}private void OnConnectedToServer()
{
    Send(response => Debug.Log(response)); 
}{% endhighlight %}

- in `OnConnectedToServer`, which is *called on client*, we send the request and pass a callback: "what to do after we get a response",
so in this case we just print the response we get to console.

{% highlight C# %}error => Debug.LogError("Something went wrong: " + error){% endhighlight %}

- The second callback is what we do if server **denies** a request. That does **not** include connection errors or any other Mirror's exceptions.
This is just for when **we** decide to deny the request and send an error message instead of a response.

{% highlight C# %}protected override void OnRequest(out RequestStatus status)
{
    res.SetResponse("Hello World!");
    status = OK;
}{% endhighlight %}

- in `OnRequest` (called on SERVER) we should process the request in some way. This time we will just set the response as "Hello World" string.

{% highlight C# %}status = OK;{% endhighlight %}

- We should pass the `status` variable out, so now nothing could get wrong so we set it to the pre-defined `OK` property which means there were no errors and response should be sent.


It's hard to find a consistent approach if you have a lot of 

Since NetworkBehaviours [don't have generics support](https://github.com/vis2k/Mirror/issues/1260), we came up with
a workaround: every time you create a new request type

*(Todo: we're working on the lower-level implementation based on mirror's [network messages](https://mirror-networking.gitbook.io/docs/guides/communications/network-messages) - 
[watch our progress])*

When you create a request, deriving from a request baseclass, 

## Brief Overview

The final gameobject designed using Modula should consist of these components:

- **[Main](/module-features#main-)** behaviour script

    
    {% highlight C# %}// Main Behaviour
    public class Car : ModularBehaviour
    {
         // Your code as you do it usually
         ...
    }{% endhighlight %}

- Some connected modules


    {% highlight C# %}// Example Module
    public class Engine : Module 
     {
         void Start() { ... }
         
         ...
     }{% endhighlight %}

- Other unity Components you need for this system

## Installation
{% if page.install_instructions %}
  {% include_relative {{ page.install_instructions }} %}
{% endif %}

There are other installation methods listed at [**"Installation"** page](/install#2-download-from-asset-store).
{: .notice}

### Updating
Check out the [full page](/install#updating) to read the update instructions.

---
# Next Steps
Code your first module by following **[Quick Start](/quick-start) instructions**.