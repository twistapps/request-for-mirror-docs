---
title: Installing Modula
permalink: /install
excerpt: "How to add Modula to your project."

author_profile: false
author: Twist Apps

install_recommended: common/installation/recommended.md
install_other: common/installation/other-methods.md
install_update: common/installation/updating.md
---

{% if page.install_recommended %}
  {% include_relative {{ page.install_recommended }} %}
{% endif %}

{% if page.install_other %}
  {% include_relative {{ page.install_other }} %}
{% endif %}

{% if page.install_update %}
  {% include_relative {{ page.install_update }} %}
{% endif %}