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

  .hero {
    display: flex;
    gap: 22px;
    align-items: flex-start;
    flex-wrap: wrap;
  }

  .hero-photo {
    flex: 0 0 150px;
  }

  .hero-photo img {
    width: 150px;
    max-width: 100%;
    border-radius: 16px;
    border: 1px solid #eee;
    display: block;
  }

  .hero-content {
    flex: 1;
    min-width: 280px;
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
    margin: 10px 0 18px 0;
    font-weight: 650;
    opacity: 0.9;
  }

  .landing-blurb {
    font-size: 1.15em;
    line-height: 1.6;
    margin: 0 0 22px 0;
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

  .landing-contact {
    margin-top: 18px;
    font-size: 1.05em;
    opacity: 0.9;
  }

  .landing-contact a {
    text-decoration: none;
    border-bottom: 1px solid #ddd;
    padding-bottom: 2px;
  }

  .landing-contact a:hover {
    border-bottom-color: #bbb;
  }
</style>

<div class="landing">
  <div class="hero">
    <div class="hero-photo">
      <img
        src="{{ '/assets/img/headshot.jpg' | relative_url }}"
        alt="Photo of Craig Dermody"
      />
    </div>

    <div class="hero-content">
      <h1 class="landing-name">Craig Dermody</h1>

      <div class="landing-subtitle">Analytics | Design | Improvement</div>

      <p class="landing-blurb">
        I build data products that help public organizations make better decisions.
      </p>

      <div class="landing-actions">
        <a class="landing-btn" href="{{ '/resume/' | relative_url }}">Review my resume</a>
        <a class="landing-btn" href="{{ '/articles/' | relative_url }}">Browse my articles</a>
        <a class="landing-btn" href="{{ '/testimonials/' | relative_url }}">Read my reviews</a>
        <a class="landing-btn" href="{{ '/projects/' | relative_url }}">See my projects</a>
      </div>

      <div class="landing-contact">
        Interested in collaboration? <a href="{{ '/contact/' | relative_url }}">Contact me</a>
      </div>
    </div>
  </div>
</div>
