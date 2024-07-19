---
layout: page
title: Projects
permalink: /projects/
tags: projects
---

<div id="projects">
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
