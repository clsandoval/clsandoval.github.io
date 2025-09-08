---
title: "Projects"
permalink: /projects/
layout: archive
collection: projects
entries_layout: grid  
---

Personal coding projects and experiments.

{% for post in site.projects %}
  {% include archive-single.html %}
{% endfor %}