---
title: "Work"
permalink: /work/
layout: collection
collection: work
entries_layout: grid
---

Computer science projects and research work.

{% for post in site.work %}
  {% include archive-single.html %}
{% endfor %}