---
layout: default
title: PolicyWork
---

<style>
.portfolio-list li { margin: 0.4rem 0; }
.small { color:#666; font-size:0.9rem; }
hr { margin: 1.25rem 0; }
</style>

<!-- Top paragraph you wanted -->
This repository is a personal project for me to better my policy writing and analysis skills. I aim to mostly focus on policy relevant to technology but overall this is meant to showcase any work I come up with.

<hr/>

<!-- Build category sections from _data/papers.yml -->
{% assign data_items = site.data.papers.items | default: empty %}
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

<p class="small">Last updated: {{ site.time | date: "%B %d, %Y" }}</p>




