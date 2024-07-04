---
layout: default
title: Contact Deepak Yadav
---

<style>
  .container {
    max-width: 800px;
    margin: 0 auto;
  }
  #contact {
    padding: 2rem;
    background-color: #f9f9f9;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
  }
  .pageTitle {
    font-size: 2rem;
    font-weight: bold;
  }
  .form-label {
    font-weight: bold;
  }
  .form-control {
    border-radius: 5px;
  }
  .btn-primary {
    background-color: #007bff;
    border-color: #007bff;
    padding: 0.5rem 2rem;
    border-radius: 5px;
  }
  .btn-primary:hover {
    background-color: #0056b3;
    border-color: #0056b3;
  }
</style>

<div class="container">
  <div id="contact" class="my-5">
    <h3 class="pageTitle text-center mb-4">Contact Me</h3>
    <div class="d-flex justify-content-center">
      <div class="col-md-6">
        <form action="https://formspree.io/f/xlekyjwb" method="POST">
          <div class="mb-3">
            <label for="email" class="form-label">Your Email:</label>
            <input type="email" name="email" class="form-control" required>
          </div>
          <div class="mb-3">
            <label for="message" class="form-label">Your Message:</label>
            <textarea name="message" class="form-control" rows="5" required></textarea>
          </div>
          <div class="text-center">
            <button type="submit" class="btn btn-primary">Send Message</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</div>
