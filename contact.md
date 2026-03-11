---
layout: default
title: Contact
---

<div class="card" style="max-width: 760px; margin: 14px auto 0 auto;">
  <h2 style="margin-top:0;">Let’s connect.</h2>
  <p>
    I’m excited to hear from you, and will reach out as soon as possible.
  </p>

  <form id="contactForm" method="POST" action="https://formspree.io/f/meerjdwl">
    <div class="field">
      <label for="email">Enter your email address</label>
      <input id="email" name="email" type="email" autocomplete="email" required placeholder="you@example.com">
    </div>

    <div class="field">
      <label for="reason">Reason for contact</label>
      <select id="reason" name="reason_for_contact" required>
        <option value="" selected disabled>Select one…</option>
        <option value="employment">Employment opportunity</option>
        <option value="networking">Networking/mentoring</option>
        <option value="probono">Pro bono consultation/development</option>
        <option value="other">Something else</option>
      </select>
    </div>

    <div class="field">
      <label for="details">Would you like to include any additional details? (optional)</label>
      <textarea id="details" name="additional_details" rows="5" placeholder="Add context, timeline, links, or anything helpful."></textarea>
    </div>

    <input type="hidden" name="page" value="{{ page.url }}">
    <input type="hidden" name="site" value="{{ site.title }}">

    <div class="actions">
      <button id="submitBtn" type="submit">Submit</button>
      <span id="status" class="status" aria-live="polite"></span>
    </div>
  </form>

  <div id="successMessage" class="card card-muted" style="display:none; margin-top: 16px;">
    <strong>Thanks — your message was sent.</strong><br>
    I’ll contact you as soon as possible.
  </div>
</div>

<style>
  /* Form-only styling (uses global font + link colors from custom.css) */
  .field { margin-bottom: 16px; }

  .field label {
    display: block;
    font-weight: 600;
    margin-bottom: 6px;
  }

  .field input, .field select, .field textarea {
    width: 100%;
    box-sizing: border-box;
    border: 1px solid #ddd;
    border-radius: 10px;
    padding: 10px 12px;
    font-size: 1rem;
    font-family: inherit;
    background: #fff;
  }

  .field input::placeholder,
  .field textarea::placeholder {
    font-size: 1rem;
    font-family: inherit;
  }

  .field input:focus, .field select:focus, .field textarea:focus {
    outline: none;
    border-color: #999;
  }

  .field textarea { resize: none; }

  .actions {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-top: 6px;
  }

  button {
    border: 1px solid #111;
    border-radius: 999px;
    padding: 10px 16px;
    font-weight: 600;
    cursor: pointer;
    background: #111;
    color: #fff;
  }

  button:disabled {
    opacity: 0.6;
    cursor: not-allowed;
  }

  .status { opacity: 0.8; font-size: 0.95em; }
</style>

<script>
  (function () {
    const form = document.getElementById('contactForm');
    const status = document.getElementById('status');
    const successMessage = document.getElementById('successMessage');
    const submitBtn = document.getElementById('submitBtn');
    const reasonSelect = document.getElementById('reason');

    // Preselect dropdown from URL query string, e.g. ?reason=employment
    const params = new URLSearchParams(window.location.search);
    const reasonFromUrl = params.get('reason');

    if (reasonFromUrl) {
      const validValues = ['employment', 'networking', 'probono', 'other'];
      if (validValues.includes(reasonFromUrl)) {
        reasonSelect.value = reasonFromUrl;
      }
    }

    form.addEventListener('submit', async function (e) {
      e.preventDefault();
      status.textContent = '';

      if (!form.reportValidity()) {
        return;
      }

      submitBtn.disabled = true;
      submitBtn.textContent = 'Submitting…';

      try {
        const formData = new FormData(form);

        const response = await fetch(form.action, {
          method: 'POST',
          body: formData,
          headers: { 'Accept': 'application/json' }
        });

        if (response.ok) {
          form.style.display = 'none';
          successMessage.style.display = 'block';
        } else {
          status.textContent = 'Something went wrong. Please try again.';
          submitBtn.disabled = false;
          submitBtn.textContent = 'Submit';
        }

      } catch (err) {
        status.textContent = 'Network error. Please try again.';
        submitBtn.disabled = false;
        submitBtn.textContent = 'Submit';
      }
    });
  })();
</script>
