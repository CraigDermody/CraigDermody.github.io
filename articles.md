---
layout: default
title: Articles
permalink: /articles/
---

<p>
  I use data and technology to improve public services and decision-making. I write about data products, digital services, and improving government. I also write as a convenient excuse to post photos of my very cute baby. If something here resonates, <a href="{{ '/contact/?reason=networking' | relative_url }}">let’s connect</a>.
</p>

<div id="search-container" class="articles-search-container"></div>
<div id="articles-feed"></div>

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

    function escapeHtml(str) {
      return String(str)
        .replace(/&/g, "&amp;")
        .replace(/</g, "&lt;")
        .replace(/>/g, "&gt;")
        .replace(/"/g, "&quot;")
        .replace(/'/g, "&#39;");
    }

    searchContainer.innerHTML = `
      <input
        id="article-search"
        class="search-input"
        type="text"
        placeholder="Search articles..."
        aria-label="Search articles"
      >
    `;

    const searchEl = document.getElementById("article-search");
    const posts = window.__ARTICLES__ || [];

    function renderFeed() {
      const q = (searchEl.value || "").toLowerCase().trim();

      const filtered = q
        ? posts.filter((p) =>
            (p.title || "").toLowerCase().includes(q) ||
            (p.excerpt || "").toLowerCase().includes(q)
          )
        : posts;

      if (filtered.length === 0) {
        feedEl.innerHTML = '<div class="empty-state">No articles match your search yet.</div>';
        return;
      }

      feedEl.innerHTML = filtered
        .map((p) => `
          <div class="card article-card">
            <div class="article-title">
              <a href="${p.url}">${escapeHtml(p.title || "")}</a>
            </div>
            <div class="article-author">Craig Dermody</div>
            <div class="article-excerpt">${escapeHtml(p.excerpt || "")}</div>
            <div class="article-date">${escapeHtml(p.dateDisplay || p.dateISO || "")}</div>
          </div>
        `)
        .join("");
    }

    renderFeed();
    searchEl.addEventListener("input", renderFeed);
  })();
</script>
