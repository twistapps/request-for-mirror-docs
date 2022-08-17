---
title: Integration
permalink: /integration
excerpt: "How to add integrate 3rd party packages with Modula."

author_profile: false
author: Twist Apps

integr_mirror: common/integrations/mirror.md
integr_modula: common/integrations/modula.md
---

# Built-In integrations
These are integrations with 3rd party packages that are supported out-of-the-box: 

## Mirror
{% if page.integr_mirror %}
  {% include_relative {{ page.integr_mirror }} %}
{% endif %}

## Modula
{% if page.integr_modula %}
    {% include_relative {{ page.integr_modula }} %}
{% endif %}