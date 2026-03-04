---
layout: page
title: Articles
permalink: /articles/
---

# Articles

Filter by topic or search to find posts by theme.

<div id="topic-filters" style="margin: 12px 0 14px 0;"></div>

<input id="article-search" type="text" placeholder="Search articles..." style="display:block; box-sizing:border-box; width:100%; max-width:520px; padding:10px 12px; border-radius:10px; border:1px solid #ddd; margin:0 0 14px 0;">

<div id="articles-feed"></div>
<script>
window.__ARTICLES__ = [
  {% assign items = site.articles | sort: "date" | reverse %}
  {% for a in items %}
  {
    title: {{ a.title | jsonify }},
    url: {{ a.url | relative_url | jsonify }},
    date: {{ a.date | date: "%Y-%m-%d" | jsonify }},
    excerpt: {{ a.excerpt | default: "" | strip_html | strip_newlines | jsonify }},
    tags: {{ a.tags | default: empty | jsonify }}
  }{% unless forloop.last %},{% endunless %}
  {% endfor %}
];

(function () {
  const filtersEl = document.getElementById("topic-filters");
  const feedEl = document.getElementById("articles-feed");
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
        <button data-tag="${tag}"
          style="margin: 6px 8px 0 0; padding: 6px 10px; border-radius: 999px; border: 1px solid #ddd; background: ${isActive ? "#f2f2f2" : "white"}; cursor: pointer;">
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
    const q = (searchEl?.value || "").toLowerCase().trim();

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
      feedEl.innerHTML = `<div style="opacity:0.7; margin-top:12px;">No articles match this filter yet.</div>`;
      return;
    }

    feedEl.innerHTML = filtered.map(p => `
      <div style="border:1px solid #eee; padding:14px; border-radius:10px; margin: 12px 0;">
        <div style="font-size:0.95em; opacity:0.75;">${p.date}</div>
        <div style="font-size:1.15em; font-weight:700; margin-top:4px;">
          <a href="${p.url}">${p.title}</a>
        </div>
        <div style="margin-top:6px;">${p.excerpt || ""}</div>
        <div style="margin-top:10px; font-size:0.9em; opacity:0.8;">
          ${p.tags.map(t => `#${prettyTag(t)}`).join("  ")}
        </div>
      </div>
    `).join("");
  }

  renderFilters();
  renderFeed();

  searchEl?.addEventListener("input", renderFeed);
})();
</script>
