---
title: Home
nav_order: 1
---

# LEVEL References

Reference material for LEVEL Motion sensors and apps.

## Guides

{% assign guides = site.pages | where_exp: "p", "p.name != 'index.md'" | where_exp: "p", "p.title" | sort: "title" %}
{% for p in guides %}
- [{{ p.title }}]({{ p.url | relative_url | replace: '.html', '' }}){% if p.description %} - {{ p.description }}{% endif %}
{% endfor %}

More guides (manuals, FAQs) will be added here over time.
