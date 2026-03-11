---
layout: default
title: Contact
---

<div class="card contact-card">
  <h2 class="contact-title">Let’s connect.</h2>
  <p>
    I’m excited to hear from you and will reach out as soon as possible.
  </p>

  <form
    id="contactForm"
    class="contact-form"
    method="POST"
    action="https://formspree.io/f/meerjdwl"
    novalidate
  >
    <div class="field">
      <label for="email">Enter your email address</label>
      <input
        id="email"
        name="email"
        type="email"
        autocomplete="email"
        required
        placeholder="you@example.com"
      >
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
      <textarea
        id="details"
        name="additional_details"
        rows="5"
        placeholder="Add context, timeline, links, or anything helpful."
      ></textarea>
    </div>

    <input type="hidden" name="page" value="{{ page.url }}">
    <input type="hidden" name="site" value="{{ site.title }}">

    <div class="actions">
      <button id="submitBtn" class="contact-submit" type="submit">Submit</button>
      <span id="status" class="status" aria-live="polite" role="status"></span>
    </div>
  </form>

  <div id="successMessage" class="card card-muted contact-success" role="status" aria-live="polite" hidden>
    <strong>Thanks — your message was sent.</strong><br>
    I’ll contact you as soon as possible.
  </div>
</div>

<script>
  (function () {
    const form = document.getElementById('contactForm');
    const status = document.getElementById('status');
    const successMessage = document.getElementById('successMessage');
    const submitBtn = document.getElementById('submitBtn');
    const reasonSelect = document.getElementById('reason');

    const params = new URLSearchParams(window.location.search);
    const reasonFromUrl = params.get('reason');
    const validValues = new Set(['employment', 'networking', 'probono', 'other']);

    if (reasonFromUrl && validValues.has(reasonFromUrl)) {
      reasonSelect.value = reasonFromUrl;
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
          headers: { Accept: 'application/json' }
        });

        if (response.ok) {
          form.hidden = true;
          successMessage.hidden = false;
          status.textContent = '';
          return;
        }

        status.textContent = 'Something went wrong. Please try again.';
      } catch (err) {
        status.textContent = 'Network error. Please try again.';
      }

      submitBtn.disabled = false;
      submitBtn.textContent = 'Submit';
    });
  })();
</script>
