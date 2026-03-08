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

  /* Headshot tall enough to visually span the name + subtitle */
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
    font-weight: 650; /* less bold */
    letter-spacing: -0.02em;
    text-transform: uppercase;
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

  .reasons {
    margin-top: 22px;
    border: 1px solid #eee;
    border-radius: 14px;
    background: #fafafa;
    padding: 16px 16px 14px 16px;
  }

  /* Make the "Contact me" header match your subtitle styling */
  .reasons-title {
    font-size: 1.55em;
    margin: 0 0 10px 0;
    font-weight: 650;
    opacity: 0.9;
  }

  .reasons ul {
    margin: 0;
    padding-left: 18px;
  }

  .reasons li {
    margin: 10px 0;
    line-height: 1.55;
  }

  .reasons a {
    text-decoration: none;
    border-bottom: 1px solid #ddd;
    padding-bottom: 2px;
    font-weight: 700;
    white-space: nowrap;
  }

  .reasons a:hover {
    border-bottom-color: #bbb;
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
      <h1 class="landing-name">CRAIG DERMODY</h1>
      <div class="landing-subtitle">Analytics | Design | Improvement</div>
    </div>
  </div>

  <p class="landing-blurb">
    <strong>I use data and technology to improve public services and decision-making.</strong>
  </p>

  <div class="landing-actions">
    <a class="landing-btn" href="{{ '/resume/' | relative_url }}">Review my resume</a>
    <a class="landing-btn" href="{{ '/articles/' | relative_url }}">Browse my articles</a>
    <a class="landing-btn" href="{{ '/testimonials/' | relative_url }}">Read my reviews</a>
    <a class="landing-btn" href="{{ '/projects/' | relative_url }}">See my projects</a>
  </div>

  <div class="reasons">
    <div class="reasons-title">Contact me</div>
    <ul>
      <li>
        I’m finishing a professional sabbatical and am actively searching for my next role.
        <a href="{{ '/contact/' | relative_url }}">Let’s talk</a>.
      </li>
      <li>
        I provide pro bono support for local government and nonprofits developing data products and digital services.
        <a href="{{ '/contact/' | relative_url }}">Let’s collaborate</a>.
      </li>
      <li>
        I’m always open to network or mentor civic tech professionals working to improve government.
        <a href="{{ '/contact/' | relative_url }}">Let’s connect</a>.
      </li>
    </ul>
  </div>
</div>
