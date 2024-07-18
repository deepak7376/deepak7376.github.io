---
layout: default
title: Deepak Yadav
---

<style>
  #articles h3 {
    font-size: 1.25rem; /* Adjust the title font size */
    margin-bottom: 0.5rem; /* Optional: Adjust spacing */
  }

  #articles .description {
    font-size: 0.875rem; /* Adjust the description font size */
    line-height: 1.4; /* Optional: Adjust line height for readability */
  }

  #articles .date {
    font-size: 0.75rem; /* Adjust the date font size */
    color: #6c757d; /* Optional: Adjust the date color */
  }
</style>

<div id="articles">
  <h3>Articles</h3>
  <ul class="posts noList">
    {%- for post in site.posts -%}
      <li>
        <span class="date">{{ post.date | date_to_string }}</span>
        <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
        <p class="description">{%- if post.description -%}{{ post.description | strip_html | strip_newlines | truncate: 120 }}{%- else -%}{{ post.content | strip_html | strip_newlines | truncate: 120 }}{%- endif -%}</p>
      </li>
    {%- endfor -%}
  </ul>
</div>
