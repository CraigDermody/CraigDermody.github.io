---
layout: default
title: Craig Dermody
---

<style>
  .landing {
    max-width: 900px;
    margin: 42px auto 0 auto;
    padding: 0 18px;
  }

  .header-row {
    display: flex;
    align-items: flex-start;
    gap: 18px;
    flex-wrap: wrap;
  }

  /* Make the headshot tall enough to visually span the name + subtitle */
  .headshot {
    width: 132px;
    height: 132px;
    border-radius: 999px;
    border: 1px solid #eee;
    object-fit: cover;
    display: block;
    flex: 0 0 132px;
  }

  .title-block {
    min-width: 260px;
    flex: 1;
  }

  .landing-name {
    font-size: 4.2em;
    line-height: 1.02;
    margin: 0;
    font-weight: 800;
    letter-spacing: -0.02em;
  }

  .landing-subtitle {
    font-size: 1.55em;
    margin: 10px 0 0 0;
    font-weight: 650;
    opacity: 0.9;
  }

  .landing-blurb {
    font-size: 1.15em;
    line-height: 1.6;
    margin: 18px 0 22px 0;
    max-width: 46em;
    opacity: 0.92;
  }

  .landing-actions {
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
    margin-top: 10px;
  }

  .landing-btn {
    display: inline-block;
    padding: 10px 16px;
    border-radius: 999px;
    border: 1px solid #ddd;
    background: #fff;
    color: #111;
    font-weight: 650;
    text-decoration: none;
  }

  .landing-btn:hover {
    border-color: #bbb;
  }

  /* Make the contact CTA pop more */
  .landing-cta {
    margin-top: 18px;
    display: inline-flex;
    align-items: center;
    gap: 10px;
    padding: 12px 14px;
    border-radius: 14px;
    border: 1px solid #eee;
    background: #fafafa;
  }

  .landing-cta-text {
    font-size: 1.05em;
    font-weight: 650;
    opacity: 0.95;
  }

  .landing-cta a {
    display: inline-block;
    padding: 8px 12px;
    border-radius: 999px;
    border: 1px solid #ddd;
    background: #fff;
    color: #111;
    font-weight: 700;
    text-decoration: none;
  }

  .landing-cta a:hover {
    border-color: #bbb;
  }
</style>

<div class="landing">
  <div class="header-row">
    <img
      class="headshot"
      src="{{ '/assets/img/headshot.jpg' | relative_url }}"
      alt="Photo of Craig Dermody"
    />

    <div class="title-block">
      <h1 class="landing-name">Craig Dermody</h1>
      <div class="landing-subtitle">Analytics | Design | Improvement</div>
    </div>
  </div>

  <p class="landing-blurb">
    I build data products that help public organizations make better decisions.
  </p>

  <div class="landing-actions">
    <a class="landing-btn" href="{{ '/resume/' | relative_url }}">Review my resume</a>
    <a class="landing-btn" href="{{ '/articles/' | relative_url }}">Browse my articles</a>
    <a class="landing-btn" href="{{ '/testimonials/' | relative_url }}">Read my reviews</a>
    <a class="landing-btn" href="{{ '/projects/' | relative_url }}">See my projects</a>
  </div>

  <div class="landing-cta">
    <div class="landing-cta-text">Interested in collaboration?</div>
    <a href="{{ '/contact/' | relative_url }}">Contact me</a>
  </div>
</div>
