---
layout: default
title: PolicyWork
---

<style>
.portfolio-list li { margin: 0.4rem 0; }
.small { color:#666; font-size:0.9rem; }
hr { margin: 1.25rem 0; }
</style>

<!-- Hero -->
This repository is a personal project for me to better my policy writing and analysis skills. I aim to focus on policy relevant to technology but overall this is meant to showcase any work I come up with.

<hr/>

<!-- Category list built from _data/papers.yml -->
{% assign data_items = site.data.papers.items | default: empty %}

{% comment %}
Order your sections here:
{% endcomment %}
{% assign category_order = "Tech Policy|Governance & National Security" | split: "|" %}

{% for cat in category_order %}
  {% assign in_cat = data_items | where: "category", cat %}
  {% if in_cat.size > 0 %}
    <h2>{{ cat }}</h2>

    {% assign pinned = in_cat | where: "pinned", true %}
    {% if pinned.size > 0 %}
    <h3>Featured</h3>
    <ul class="portfolio-list">
      {% for p in pinned %}
        <li><a href="{{ '/pdfs/' | append: p.file | uri_escape | relative_url }}" target="_blank" rel="noopener">{{ p.title }}</a></li>
      {% endfor %}
    </ul>
    {% endif %}

    {% assign rest = in_cat | where_exp: "item", "item.pinned != true" %}
    {% if rest.size > 0 %}
    <ul class="portfolio-list">
      {% for p in rest %}
        <li><a href="{{ '/pdfs/' | append: p.file | uri_escape | relative_url }}" target="_blank" rel="noopener">{{ p.title }}</a></li>
      {% endfor %}
    </ul>
    {% endif %}
  {% endif %}
{% endfor %}

{% comment %}
Auto-catch any PDFs in /pdfs that aren't listed in _data/papers.yml, under an "Additional Papers" section.
{% endcomment %}
{% assign mapped_files = data_items | map: "file" %}
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
<h2>Additional Papers</h2>
<ul class="portfolio-list">
  {% for f in unmapped %}
    <li><a href="{{ f.path | uri_escape | relative_url }}" target="_blank" rel="noopener">
      {{ f.name | replace: '-', ' ' | replace: '_', ' ' | replace: '.pdf','' }}
    </a></li>
  {% endfor %}
</ul>
{% endif %}

<p class="small">Last updated: {{ site.time | date: "%B %d, %Y" }}</p>

</ul>
{% endif %}

<p class="small">Last updated: {{ site.time | date: "%B %d, %Y" }}</p>


