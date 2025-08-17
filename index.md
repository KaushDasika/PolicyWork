---
layout: default
title: PolicyWork
---

{% comment %}
Reuse your repo README at the top of the website
{% endcomment %}
{% include_relative README.md %}

---

## Downloads (PDFs)
<!-- Lists any .pdf inside /pdfs, newest-first if you date-prefix filenames -->
{% assign pdfs = site.static_files | where: "extname", ".pdf" | sort: "name" | reverse %}
<ul>
{% for f in pdfs %}
  {% if f.path contains '/pdfs/' %}
  <li>
    <a href="{{ f.path | relative_url }}" target="_blank" rel="noopener">
      {{ f.name | replace: '-', ' ' | replace: '_', ' ' | replace: '.pdf', '' }}
    </a>
  </li>
  {% endif %}
{% endfor %}
</ul>

_Last updated: {{ site.time | date: "%B %d, %Y" }}_
