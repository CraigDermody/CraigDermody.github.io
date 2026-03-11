---
layout: default
title: Articles
permalink: /articles/
---

<p>
  I build data tools and dashboards that help governments make better decisions. Topics include data product development, designing for public-sector users, and practical civic tech project ideas. If something here resonates, <a href="{{ '/contact/?reason=networking' | relative_url }}">let’s connect</a>.
</p>

<div id="search-container" style="margin: 12px 0 14px 0;"></div>
<div id="articles-feed"></div>

<style>
  /* Page-specific (kept minimal; uses global styles from custom.css) */
  .search-input {
    display: block;
    box-sizing: border-box;
    width: 100%;
    max-width: 520px;
    padding: 10px 12px;
    border-radius: 10px;
    border: 1px solid #ddd;
    font-size: 1rem;
    font-family: inherit;
    background: #fff;
  }
  .search-input:focus { outline: none; border-color: #bbb; }

  .article-title { font-size: 1.15em; font-weight: 800; margin: 0; }
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
      <div class="card" style="margin: 12px 0;">
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
