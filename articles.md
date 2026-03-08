---
layout: default
title: Articles
permalink: /articles/
---

<div class="articles-intro">
  <p class="articles-lede">
    I build data tools and dashboards that help governments make better decisions. My writing focuses on what actually works in practice—BI and dashboard design, data modeling and ETL, reporting automation, performance measurement, and user-centered design. If something here resonates, <a href="{{ '/contact/' | relative_url }}">let’s connect</a>.
  </p>
</div>

<div id="search-container" class="search-container"></div>
<div id="articles-feed" class="articles-feed"></div>

<style>
  .articles-intro { margin: 6px 0 14px 0; }
  .articles-lede { margin: 0 0 14px 0; line-height: 1.6; max-width: 58em; }

  .search-container { margin: 0 0 14px 0; }
  .search-input {
    display: block;
    box-sizing: border-box;
    width: 100%;
    max-width: 520px;
    padding: 10px 12px;
    border-radius: 10px;
    border: 1px solid #ddd;
  }
  .search-input:focus { outline: none; border-color: #bbb; }

  .article-card {
    border: 1px solid #eee;
    padding: 14px;
    border-radius: 10px;
    margin: 12px 0;
    background: #fff;
  }

  .article-title { font-size: 1.15em; font-weight: 800; margin-top: 0; }
  .article-title a { text-decoration: none; }
  .article-title a:hover { text-decoration: underline; }

  .article-author { margin-top: 6px; font-size: 0.95em; opacity: 0.85; }

  .article-excerpt { margin-top: 8px; line-height: 1.55; }

  .article-date { margin-top: 10px; font-size: 0.95em; opacity: 0.75; }

  .empty-state { opacity: 0.7; margin-top: 12px; }
</style>

<script>
window.__ARTICLES__ = [
  {% assign items = site.articles | sort: "date" | reverse %}
  {% for a in items %}
  {
    title: {{ a.title | jsonify }},
    url: {{ a.url | relative_url | jsonify }},
    dateISO: {{ a.date | date: "%Y-%m-%d" | jsonify }},
    dateDisplay: {{ a.date | date: "%b %-d, %Y" | jsonify }},
    excerpt: {{ a.excerpt | default: "" | strip_html | strip_newlines | jsonify }}
  }{% unless forloop.last %},{% endunless %}
  {% endfor %}
];

(function () {
  const searchContainer = document.getElementById("search-container");
  const feedEl = document.getElementById("articles-feed");

  searchContainer.innerHTML = `
    <input id="article-search" class="search-input" type="text" placeholder="Search articles..." aria-label="Search articles">
  `;
  const searchEl = document.getElementById("article-search");

  const posts = (window.__ARTICLES__ || []);

  function renderFeed() {
    const q = (searchEl.value || "").toLowerCase().trim();

    const filtered = q
      ? posts.filter(p =>
          (p.title || "").toLowerCase().includes(q) ||
          (p.excerpt || "").toLowerCase().includes(q)
        )
      : posts;

    if (filtered.length === 0) {
      feedEl.innerHTML = `<div class="empty-state">No articles match your search yet.</div>`;
      return;
    }

    feedEl.innerHTML = filtered.map(p => `
      <div class="article-card">
        <div class="article-title">
          <a href="${p.url}">${p.title}</a>
        </div>
        <div class="article-author">Craig Dermody</div>
        <div class="article-excerpt">${p.excerpt || ""}</div>
        <div class="article-date">${p.dateDisplay || p.dateISO || ""}</div>
      </div>
    `).join("");
  }

  renderFeed();
  searchEl.addEventListener("input", renderFeed);
})();
</script>
