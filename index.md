---
layout: default
title: PolicyWork
---

<style>
/* light, theme-friendly polish */
.portfolio-list { list-style: none; padding-left: 0; }
.portfolio-list li { margin: 0.5rem 0; }
.portfolio-list a { text-decoration: none; }
.badge { font-size: 0.8rem; padding: 0.15rem 0.4rem; border: 1px solid #ccc; border-radius: 6px; margin-left: 0.5rem; }
.small { color:#666; font-size:0.9rem; }
hr { margin: 1.25rem 0; }
</style>

<!-- Your hero paragraph -->
This repository is a personal project for me to better my policy writing and analysis skills. I aim to mostly focus on policy relevant to technology but overall this is meant to showcase any work I come up with.

<hr/>

<!-- Build category sections from _data/papers.yml -->
{% assign data_items = site.data.papers.items | default: empty %}

{% comment %}
Order your sections here. Rename the second one if you prefer:
e.g., "Public Administration & Security" or "Governance & National Security"
{% endcomment %}
{% assign category_order = "Tech Policy|Governance & National Security" | split: "|" %}

{% for cat in category_order %}
  {% assign in_cat = data_items | where: "category", cat %}
  {% if in_cat.size > 0 %}
    <h2>{{ cat }}</h2>
    <ul class="portfolio-list">
      {%- comment -%} pinned first with badge {%- endcomment -%}
      {% for p in in_cat %}
        {% if p.pinned %}
          <li>
            <a href="{{ '/pdfs/' | append: p.file | uri_escape | relative_url }}" target="_blank" rel="noopener">{{ p.title }}</a>
            <span class="badge">Featured</span>
          </li>
        {% endif %}
      {% endfor %}
      {%- comment -%} then the rest {%- endcomment -%}
      {% for p in in_cat %}
        {% unless p.pinned %}
          <li><a href="{{ '/pdfs/' | append: p.file | uri_escape | relative_url }}" target="_blank" rel="noopener">{{ p.title }}</a></li>
        {% endunless %}
      {% endfor %}
    </ul>
  {% endif %}
{% endfor %}

{% comment %}
Auto-catch any PDFs in /pdfs not listed in _data/papers.yml
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


<p class="small">Last updated: {{ site.time | date: "%B %d, %Y" }}</p>




