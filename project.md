---
layout: page
title: Project
---

## Projects I've done:

{% for project in site.project %}
  * {{ project.date | date_to_string }} &raquo; [ {{ project.title }} ]({{ project.url }})
{% endfor %}

If you like my website, follow me on twitter [@vincetallica](https://twitter.com/vincetallica).
