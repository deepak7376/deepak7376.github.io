---
layout: default
title: Contact Deepak Yadav
---

<div id="contact">
  <h3 class="pageTitle">Contact Me</h3>
  <div class="form-container">
    <!-- modify this form HTML and place wherever you want your form -->
      <form
        action="https://formspree.io/f/xlekyjwb"
        method="POST"
      >
        <label>
          Your email:
          <input type="email" name="email">
        </label>
        <label>
          Your message:
          <textarea name="message"></textarea>
        </label>
        <!-- your other form fields go here -->
        <button type="submit">Send</button>
      </form>
  </div>
</div>

<style>
.form-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}
</style>
