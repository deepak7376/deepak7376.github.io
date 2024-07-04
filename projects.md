---
layout: default
title: Deepak Yadav
---

<style>
  #projects {
    padding: 2rem;
    background-color: #f9f9f9;
  }
  .pageTitle {
    font-size: 2rem;
    font-weight: bold;
    margin-bottom: 1.5rem;
  }
  .card {
    border: 1px solid #ddd;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
    overflow: hidden;
    margin-bottom: 1.5rem;
    background-color: #fff;
    transition: box-shadow 0.3s ease;
  }
  .card:hover {
    box-shadow: 0 0 15px rgba(0,0,0,0.2);
  }
  .card-body {
    padding: 1.5rem;
  }
  .card-title {
    font-size: 1.25rem;
    font-weight: bold;
    margin-bottom: 0.5rem;
  }
  .card-text {
    font-size: 1rem;
    color: #555;
    margin-bottom: 1rem;
  }
  .card-link {
    color: #007bff;
    text-decoration: none;
  }
  .card-link:hover {
    text-decoration: underline;
  }
</style>

<div id="projects">
  <h3 class="pageTitle">Recent Projects</h3>
  <div class="row">
    {% for project in site.data.projects %}
    <div class="col-md-4">
      <div class="card">
        <div class="card-body">
          <h4 class="card-title">{{ project.name }}</h4>
          <p class="card-text">{{ project.description }}</p>
          <a href="{{ project.link }}" class="card-link" target="_blank">GitHub link</a>
        </div>
      </div>
    </div>
    {% endfor %}
  </div>
</div>
