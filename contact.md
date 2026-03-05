---
layout: default
title: Contact
---

<div class="contact-wrap">
  <div class="contact-card">
    <h2 style="margin-top:0;">Contact</h2>
    <p style="margin-bottom:18px;">
      Send a message using the form below. I’ll get back to you as soon as possible.
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
          <option value="Consulting/product development (local government, nonprofit, and academia)">
            Consulting/product development (local government, nonprofit, and academia)
          </option>
          <option value="Consulting/product development (private sector)">
            Consulting/product development (private sector)
          </option>
          <option value="Employment opportunity">Employment opportunity</option>
          <option value="Other">Other</option>
        </select>
      </div>

      <div class="field" id="otherField" style="display:none;">
        <label for="otherReason">If “Other,” please specify</label>
        <input id="otherReason" name="other_reason" type="text" placeholder="Type your reason">
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

    <div id="successMessage" class="success" style="display:none;">
      <strong>Thanks — your message was sent.</strong><br>
      I’ll contact you as soon as possible.
    </div>
  </div>
</div>

<style>
  .contact-wrap {
    margin-top: 14px;
    display: flex;
    justify-content: center;
  }

  .contact-card {
    width: 100%;
    max-width: 760px;
    border: 1px solid #eee;
    border-radius: 14px;
    padding: 22px;
    box-shadow: 0 6px 24px rgba(0,0,0,0.04);
    background: #fff;
  }

  .field { margin-bottom: 16px; }

  .field label {
    display: block;
    font-weight: 600;
    margin-bottom: 6px;
  }

  .field input, .field select, .field textarea {
    width: 100%;
    border: 1px solid #ddd;
    border-radius: 10px;
    padding: 10px 12px;
    font-size: 1rem;
    background: #fff;
  }

  .field input:focus, .field select:focus, .field textarea:focus {
    outline: none;
    border-color: #999;
  }

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

  .success {
    margin-top: 16px;
    padding: 14px 14px;
    border: 1px solid #e6e6e6;
    border-radius: 12px;
    background: #fafafa;
  }
</style>

<script>
  (function () {
    const form = document.getElementById('contactForm');
    const reason = document.getElementById('reason');
    const otherField = document.getElementById('otherField');
    const otherReason = document.getElementById('otherReason');
    const status = document.getElementById('status');
    const successMessage = document.getElementById('successMessage');
    const submitBtn = document.getElementById('submitBtn');

    function toggleOther() {
      const isOther = reason.value === 'Other';
      otherField.style.display = isOther ? 'block' : 'none';
      otherReason.required = isOther;
      if (!isOther) otherReason.value = '';
    }

    reason.addEventListener('change', toggleOther);
    toggleOther();

    form.addEventListener('submit', async function (e) {
      e.preventDefault();
      status.textContent = '';

      // Enforce HTML5 validation before sending
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

        const data = await response.json().catch(() => null);

        if (response.ok) {
          form.style.display = 'none';
          successMessage.style.display = 'block';
          return;
        }

        // Show real Formspree error if available
        if (data && data.errors && data.errors.length) {
          status.textContent = data.errors.map(e => e.message).join(' ');
        } else if (data && data.error) {
          status.textContent = data.error;
        } else {
          status.textContent = 'Something went wrong. Please try again.';
        }

        submitBtn.disabled = false;
        submitBtn.textContent = 'Submit';

      } catch (err) {
        status.textContent = 'Network error. Please try again.';
        submitBtn.disabled = false;
        submitBtn.textContent = 'Submit';
      }
    });
  })();
</script>
