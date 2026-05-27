---
layout: home
title: Policy Portfolio
---

<div class="hero-section">
  <div class="hero-noise"></div>
  <div class="hero-glow glow-1"></div>
  <div class="hero-glow glow-2"></div>
  <div class="hero-content">
    <div class="hero-eyebrow">
      <span class="eyebrow-dot"></span>
      Policy Researcher &amp; Analyst
    </div>
    <h1 class="hero-name">Kaushal<br>Dasika</h1>
    <div class="hero-divider"></div>
    <p class="hero-tags">
      <span>Artificial Intelligence</span>
      <span>Technology Governance</span>
      <span>National Security</span>
      <span>Data Analysis</span>
    </p>
    <p class="hero-description">
      Research and policy analysis at the intersection of emerging technology,
      governance, and national security — examining how institutions adapt to a
      rapidly shifting technological landscape.
    </p>
  </div>
</div>

<section class="publications-section">
  <div class="section-header">
    <span class="section-label">Work</span>
    <h2>Publications &amp; Research</h2>
  </div>

  {% assign categories = site.data.papers.items | map: "category" | uniq %}
  {% for category in categories %}
  {% assign cat_papers = site.data.papers.items | where: "category", category %}
  {% if cat_papers.size > 0 %}
  <div class="category-block">
    <div class="category-label">{{ category }}</div>
    <div class="paper-list">
      {% for paper in cat_papers %}
      <a class="paper-row" href="{{ site.baseurl }}/pdfs/{{ paper.file | uri_escape }}">
        <div class="paper-row-inner">
          <div class="paper-row-text">
            <span class="paper-row-title">{{ paper.title }}</span>
            {% if paper.pinned %}
            <span class="paper-badge">Featured</span>
            {% endif %}
          </div>
          <div class="paper-row-arrow">
            <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M4 10H16M16 10L11 5M16 10L11 15" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </div>
        </div>
        <div class="paper-row-bar"></div>
      </a>
      {% endfor %}
    </div>
  </div>
  {% endif %}
  {% endfor %}

  <div class="category-block">
    <div class="category-label">Political Data Analysis</div>
    <div class="paper-list">
      <a class="paper-row" href="https://kaushdasika.github.io/ps270-final-project/" target="_blank" rel="noopener">
        <div class="paper-row-inner">
          <div class="paper-row-text">
            <span class="paper-row-title">Markets, Approval, and Incumbent Presidential Re-election</span>
            <span class="paper-meta">Analysis of stock market performance and presidential approval during reelection campaigns</span>
          </div>
          <div class="paper-row-arrow">
            <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M4 10H16M16 10L11 5M16 10L11 15" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </div>
        </div>
        <div class="paper-row-bar"></div>
      </a>
    </div>
  </div>
</section>

<footer class="site-footer-custom">
  <span>Kaushal Dasika</span>
  <span class="footer-sep">·</span>
  <span>Policy &amp; Research</span>
</footer>
