---
layout: default
title: Articles
permalink: /articles/
---

<div class="articles-intro">
  <p class="articles-lede">
    <strong>Writing on public-sector analytics, data products, and service delivery.</strong>
    These posts share practical lessons from building dashboards, reporting workflows, and decision-support tools in government—where usability, trust, and maintainability matter as much as the numbers.
  </p>
  <p class="articles-help">
    Use topic filters or search to find posts by theme.
  </p>
</div>

<div id="topic-filters" class="topic-filters"></div>
<div id="search-container" class="search-container"></div>
<div id="articles-feed" class="articles-feed"></div>

<style>
  .articles-intro { margin: 6px 0 14px 0; }
  .articles-lede { margin: 0 0 8px 0; line-height: 1.6; max-width: 54em; }
  .articles-help { margin: 0 0 14px 0; opacity: 0.85; }

  .topic-filters { margin: 10px 0 14px 0; }
  .filter-btn {
    margin: 6px 8px 0 0;
    padding: 6px 10px;
    border-radius: 999px;
    border: 1px solid #ddd;
    background: #fff;
    cursor: pointer;
    font-weight: 650;
  }
  .filter-btn:hover { border-color: #bbb; }
  .filter-btn.active { background: #f2f2f2; }

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
  .article-date { font-size: 0.95em; opacity: 0.75; }
  .article-title { font-size: 1.15em; font-weight: 800; margin-top: 4px; }
  .article-title a { text-decoration: none; }
  .article-title a:hover { text-decoration: underline; }
  .article-excerpt { margin-top: 6px; line-height: 1.55; }
  .article-tags { margin-top: 10px; font-size: 0.9em; opacity: 0.8; }
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
    excerpt: {{ a.excerpt | default: "" | strip_html | strip_newlines | jsonify }},
    tags: {{ a.tags | default: empty | jsonify }}
  }{% unless forloop.last %},{% endunless %}
  {% endfor %}
];

(function () {
  const filtersEl = document.getElementById("topic-filters");
  const searchContainer = document.getElementById("search-container");
  const feedEl = document.getElementById("articles-feed");

  searchContainer.innerHTML = `
    <input id="article-search" class="search-input" type="text" placeholder="Search articles..." aria-label="Search articles">
  `;
  const searchEl = document.getElementById("article-search");

  const posts = (window.__ARTICLES__ || []).map(p => ({
    ...p,
    tags: Array.isArray(p.tags) ? p.tags : []
  }));

  const uniq = (arr) => Array.from(new Set(arr)).sort();
  const tagList = uniq(posts.flatMap(p => p.tags));
  let activeTag = "all";

  function prettyTag(t) { return String(t || "").replaceAll("-", " "); }

  function renderFilters() {
    const buttons = ["all", ...tagList].map(tag => {
      const isActive = tag === activeTag;
      return `
        <button class="filter-btn ${isActive ? "active" : ""}" data-tag="${tag}">
          ${tag === "all" ? "All topics" : prettyTag(tag)}
        </button>
      `;
    }).join("");

    filtersEl.innerHTML = buttons;

    filtersEl.querySelectorAll("button").forEach(btn => {
      btn.addEventListener("click", () => {
        activeTag = btn.getAttribute("data-tag");
        renderFilters();
        renderFeed();
      });
    });
  }

  function renderFeed() {
    const q = (searchEl.value || "").toLowerCase().trim();

    const filteredByTag = activeTag === "all"
      ? posts
      : posts.filter(p => p.tags.includes(activeTag));

    const filtered = q
      ? filteredByTag.filter(p =>
          (p.title || "").toLowerCase().includes(q) ||
          (p.excerpt || "").toLowerCase().includes(q) ||
          (p.tags || []).join(" ").toLowerCase().includes(q)
        )
      : filteredByTag;

    if (filtered.length === 0) {
      feedEl.innerHTML = `<div class="empty-state">No articles match this filter yet.</div>`;
      return;
    }

    feedEl.innerHTML = filtered.map(p => {
      const tagsHtml = (p.tags && p.tags.length)
        ? `<div class="article-tags">${p.tags.map(t => `#${prettyTag(t)}`).join("  ")}</div>`
        : "";

      return `
        <div class="article-card">
          <div class="article-date">${p.dateDisplay || p.dateISO || ""}</div>
          <div class="article-title">
            <a href="${p.url}">${p.title}</a>
          </div>
          <div class="article-excerpt">${p.excerpt || ""}</div>
          ${tagsHtml}
        </div>
      `;
    }).join("");
  }

  renderFilters();
  renderFeed();
  searchEl.addEventListener("input", renderFeed);
})();
</script>
