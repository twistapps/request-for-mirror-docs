---

title: Serializable Data Types
permalink: /data-types
excerpt: "We've found a workaround."

author_profile: false
author: Twist Apps

---

Currently Request uses [JsonUtility](https://docs.unity3d.com/ScriptReference/JsonUtility.html) to serialize/deserialize data.
When defining a new request, both request and response types could be set to any type that could be serialized to json.

[We are working](/todo) on integrating Mirror's serializer to handle requests. When that feature is ready,
you will be able to change the serializer option in package's settings.