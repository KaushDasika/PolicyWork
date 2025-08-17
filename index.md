---
layout: default
title: PolicyWork
---

<style>
/* light spacing polish */
.portfolio-list li { margin: 0.4rem 0; }
.small { color:#666; font-size:0.9rem; }
hr { margin: 1.25rem 0; }
</style>

<!-- Hero -->
**PolicyWork** — concise, source-cited analyses on technology & governance.

<hr/>

## Downloads (PDFs)

{% comment %}
Uses _data/papers.yml for exact titles + order.
Example:
items:
  - title: "America’s AI Push in the Big Beautiful Bill"
    file: "America’s AI Push in the Big Beautiful Bill.pdf"
    pinned: true
  - title: "Deception & Dual-Use: India’s Complicated History with Rockets"
    file: "Deception and Dual-use_ India’s Complicated History with Rockets.pdf"
{% endcomment %}

{% assign data_items = site.data.papers.items | default: empty %}
{% assign mapped_files = data_items | map: "file" %}
{% assign pinned = data_items | where: "pinned", true %}

{% if data_items.size > 0 %}

{% if pinned.size > 0 %}
### Featured
<ul class="portfolio-list">
{% for p in data_items %}
{% if p.pinned %}
  <li><a href="{{ '/pdfs/' | append: p.file | uri_escape | relative_url }}" target="_blank" rel="noopener">{{ p.title }}</a></li>
{% endif %}
{% endfor %}
</ul>
{% endif %}

### All
<ul class="portfolio-list">
{% for p in data_items %}
{% unless p.pinned %}
  <li><a href="{{ '/pdfs/' | append: p.file | uri_escape | relative_url }}" target="_blank" rel="noopener">{{ p.title }}</a></li>
{% endunless %}
{% endfor %}
</ul>

{% assign allpdfs = site.static_files | where: "extname", ".pdf" %}
{% assign unmapped = "" | split: "" %}
{% for f in allpdfs %}
  {% if f.path contains '/pdfs/' %}
    {% assign base = f.path | split: '/pdfs/' | last %}
    {% unless mapped_files contains base %}
      {% assign unmapped = unmapped | push: f %}
    {% endunless %}
  {% endif %}
{% endfor %}

{% if unmapped.size > 0 %}
### More
<ul class="portfolio-list">
{% for f in unmapped %}
  <li><a href="{{ f.path | uri_escape | relative_url }}" target="_blank" rel="noopener">
    {{ f.name | replace: '-', ' ' | replace: '_', ' ' | replace: '.pdf','' }}
  </a></li>
{% endfor %}
</ul>
{% endif %}

{% else %}
<!-- Fallback if there's no _data/papers.yml yet -->
<ul class="portfolio-list">
{% assign pdfs = site.static_files | where: "extname", ".pdf" | sort: "name" | reverse %}
{% for f in pdfs %}
  {% if f.path contains '/pdfs/' %}
    <li><a href="{{ f.path | uri_escape | relative_url }}" target="_blank" rel="noopener">
      {{ f.name | replace: '-', ' ' | replace: '_', ' ' | replace: '.pdf','' }}
    </a></li>
  {% endif %}
{% endfor %}
</ul>
{% endif %}

<p class="small">Last updated: {{ site.time | date: "%B %d, %Y" }}</p>


