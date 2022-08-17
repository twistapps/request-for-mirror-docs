---

title: What is Request?
permalink: /
excerpt: "Modula package brings the concept of Modular Entities into Unity Engine."

author_profile: true
author: Twist Apps

install_instructions: common/installation/recommended.md

---

{{site.data.package.displayname}} is a package that extends functionality of 
[Mirror&nbsp;Networking](https://mirror-networking.com/) for [Unity&nbsp;Engine](https://unity.com), 
allowing you to define http-like requests with automatic callbacks on response. 
[Get Started](#installation){: .btn .btn--primary .btn--primary .btn--info}

---
![logo](/assets/img/request-banner2.jpg)

---

Currently there are two types of requests: `Fetch<TRequest>` and `Post<TRequest,TResponse>`. 
They mimic `GET` and `POST` functionality from Http protocol respectively: 
**Fetch** comes with no request body and **Post** should have some data sent to the server.

## How this Works
Under the hood this package uses Mirror's high level `[Command]`'s 
and `[TargetRPC]` calls to exchange data between server and client, [with a catch](/under-the-hood) 
to make it possible to use in derived classes.

### Creating a request with Request

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

### Generic type Parameters Are:

- For **Post**:
{% highlight C# %}Post<RequestType, ResponseType1, ResponseType2, ResponseType3, ResponseType4>{% endhighlight %}
_Responses 2..4 are optional._

- **Fetch** has a single generic type parameter which is the Response Type.

**RequestType** is what server accepts as *request data*.<br />
**ResponseType** is what _client_ expects to get back from server as a response. <br />
_(as we specify `string` as response type in the example above)_

---

### Why use Request instead of standard Mirror workflow?
Imagine there's some data you need to get from a server,
but you don't want to synchronize it with [SyncVar]s repeatedly
(if that data is rarely needed or to abolish some possibilities to cheat).

Then there are two possible solutions:
- [Interest Management](https://mirror-networking.gitbook.io/docs/interest-management/custom) -
  this is too complex for simple things
- *Making a pair of Command (to send data) and an RPC (to receive a response)* -
  this becomes messy if you have a lot of requests to handle, and it's just exhausting to try to keep everything consistent
  in terms of naming and functionality.
  Resulting method pairs still look too decoupled after all.
- *Using lower level Network Messages* - but we want something **dead simple**, right?


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
Create your first request by following **[Quick Start](/quick-start) instructions**.