---
layout: default
title: Home
---

# D.O.C.E.T

### Latest posts

{% for p in site.posts %}
* {{ p.date | date_to_string }}: [{{ p.title }}]({{ p.url }})
{% endfor %}
