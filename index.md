---
layout: home
title: Policy Portfolio
---

<div class="hero-section">
  <div class="hero-overlay">

    <h1>Kaushal Dasika</h1>

    <p class="hero-subtitle">
      Technology Policy • Governance • Artificial Intelligence • Data Analysis
    </p>

    <p class="hero-description">
      Research and policy analysis focused on artificial intelligence governance,
      technology regulation, national security, institutional modernization,
      and political data analysis.
    </p>

  </div>
</div>

# Featured Research

<div class="paper-grid">

{% assign pinned = site.data.papers.items | where: "pinned", true %}

{% for paper in pinned %}

<div class="paper-card featured">

  <div class="paper-category">
    {{ paper.category }}
  </div>

  <h2>{{ paper.title }}</h2>

  <a class="paper-button"
     href="{{ site.baseurl }}/pdfs/{{ paper.file }}">
    Read Paper
  </a>

</div>

{% endfor %}

</div>

# All Publications

{% assign categories = site.data.papers.items | map: "category" | uniq %}

{% for category in categories %}

{% assign nonpinned = site.data.papers.items
   | where: "category", category
   | where_exp: "paper", "paper.pinned != true" %}

{% if nonpinned.size > 0 %}

## {{ category }}

<div class="paper-grid">

{% for paper in nonpinned %}

<div class="paper-card">

  <div class="paper-category">
    {{ paper.category }}
  </div>

  <h3>{{ paper.title }}</h3>

  <a class="paper-button"
     href="{{ site.baseurl }}/pdfs/{{ paper.file }}">
    Open PDF
  </a>

</div>

{% endfor %}

</div>

{% endif %}
{% endfor %}

# Data & Analysis

<div class="paper-grid">

<div class="paper-card analytics-card">

  <div class="paper-category">
    Political Data Analysis
  </div>

  <h3>
    Markets, Approval, and Incumbent Presidential Re-election
  </h3>

  <p>
    Analysis of the relationship between stock market performance
    and presidential approval ratings during reelection campaigns.
  </p>

  <a class="paper-button"
     href="https://kaushdasika.github.io/ps270-final-project/">
    View Project
  </a>

</div>

</div>
