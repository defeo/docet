---
title: Home
---

# {{ site.title }} <span class="subtitle">{{ site.tagline }}</span>


{% for p in site.posts %}
[{{ p.title }}]({{site.baseurl}}{{ p.url }})
: {{ p.date | date_to_string }} — *{{ p.description }}*
{% endfor %}
