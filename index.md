---
layout: default
title: PolicyWork
---

{%- comment -%}
Top section: reuse your repo README on the website.
{%- endcomment -%}
{% include_relative README.md %}

---

## Downloads (PDFs)

{%- comment -%}
If you maintain a manual list in _data/papers.yml, we honor that order/titles.
Items can include: 
  - title: "Nice Title"
  - file: "Exact Filename.pdf"
  - pinned: true   # to keep an item at the top
Any PDFs not listed there will appear under "More" automatically.
{%- endcomment -%}

{%- assign data_items = site.data.papers.items | default: empty -%}
{%- assign mapped_files = data_items | map: "file" -%}
{%- assign pinned = data_items | where: "pinned", true -%}

{%- if data_items.size > 0 -%}

{%- if pinned.size > 0 -%}
### Featured
<ul>
{%- for p in data_items -%}
  {%- if p.pinned -%}
    <li><a href="{{ '/pdfs/' | append: p.file | uri_escape | relative_url }}" target="_blank" rel="noopener">{{ p.title }}</a></li>
  {%- endif -%}
{%- endfor -%}
</ul>
{%- endif -%}

### All (ordered)
<ul>
{%- for p in data_items -%}
  {%- unless p.pinned -%}
    <li><a href="{{ '/pdfs/' | append: p.file | uri_escape | relative_url }}" target="_blank" rel="noopener">{{ p.title }}</a></li>
  {%- endunless -%}
{%- endfor -%}
</ul>

{%- comment -%}
Auto-list any PDFs living in /pdfs that aren't in the data file.
{%- endcomment -%}
{%- assign allpdfs = site.static_files | where: "extname", ".pdf" -%}
{%- assign unmapped = "" | split: "" -%}
{%- for f in allpdfs -%}
  {%- if f.path contains '/pdfs/' -%}
    {%- assign base = f.path | split: '/pdfs/' | last -%}
    {%- unless mapped_files contains base -%}
      {%- assign unmapped = unmapped | push: f -%}
    {%- endunless -%}
  {%- endif -%}
{%- endfor -%}

{%- if unmapped.size > 0 -%}
### More
<ul>
{%- for f in unmapped -%}
  <li><a href="{{ f.path | uri_escape | relative_url }}" target="_blank" rel="noopener">
    {{ f.name | replace: '-', ' ' | replace: '_', ' ' | replace: '.pdf', '' }}
  </a></li>
{%- endfor -%}
</ul>
{%- endif -%}

{%- else -%}
{%- comment -%}
Fallback if there's no _data/papers.yml: just list all PDFs in /pdfs by name (newest-first if you date-prefix filenames).
{%- endcomment -%}
<ul>
{%- assign pdfs = site.static_files | where: "extname", ".pdf" | sort: "name" | reverse -%}
{%- for f in pdfs -%}
  {%- if f.path contains '/pdfs/' -%}
  <li><a href="{{ f.path | uri_escape | relative_url }}" target="_blank" rel="noopener">
    {{ f.name | replace: '-', ' ' | replace: '_', ' ' | replace: '.pdf', '' }}
  </a></li>
  {%- endif -%}
{%- endfor -%}
</ul>
{%- endif -%}

_Last updated: {{ site.time | date: "%B %d, %Y" }}_

