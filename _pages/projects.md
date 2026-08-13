---
layout: page
title: projects
permalink: /projects/
description: 
nav: true
nav_order: 3
#display_categories: [recent, past]
horizontal: false
---
<style>
  /* Force fixed 1:1 ratio on card thumbnails without breaking layout height */
  .projects .card img,
  .projects .card figure img,
  .projects .card picture img {
    width: 100% !important;
    height: 100% !important;
    aspect-ratio: 4 / 3 !important;
    object-fit: cover !important;
    object-position: center !important;
  }

  /* Prevent figure containers from collapsing */
  .projects .card figure,
  .projects .card picture {
    display: block !important;
    width: 100% !important;
    aspect-ratio: 4 / 3 !important;
  }
</style>

<!-- pages/projects.md -->
<div class="projects">
{% if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>
  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
  {% endfor %}

{% else %}

<!-- Display projects without categories -->

{% assign sorted_projects = site.projects | sort: "importance" %}

  <!-- Generate cards for each project -->

{% if page.horizontal %}

  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
{% endif %}
</div>
