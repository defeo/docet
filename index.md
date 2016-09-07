---
title: Home
---

# D.O.C.E.T

### Latest posts

{% for p in site.posts %}
* {{ p.date | date_to_string }}: [{{ p.title }}]({{site.baseurl}}{{ p.url }})
{% endfor %}
