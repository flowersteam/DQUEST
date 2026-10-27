---
layout: page
title: Projects
permalink: /projects
---

<div class="project-list">
  {% for post in site.posts %}
  {% assign status_parts = post.status | split: '(' %}
  {% assign status_base = status_parts[0] | strip %}
  {% assign status_key = status_base | downcase | replace: ' ', '-' %}
  <a href="{{ post.url | relative_url }}" class="project-card{% if status_key == 'completed' %} project-card--completed{% endif %}">
    <div class="project-card__body">
      <h3 class="project-card__title">{{ post.title }}</h3>
      {% if post.people %}
      <p class="project-card__people">
        <i class="fas fa-users" aria-hidden="true"></i>
        {{ post.people | join: ", " }}
      </p>
      {% endif %}
      <p class="project-card__summary">{{ post.summary }}</p>
    </div>
    {% if post.thumbnail %}
    <div class="project-card__thumbnail">
      <img src="{{ post.thumbnail | relative_url }}" alt="{{ post.title }}" />
    </div>
    {% endif %}
    {% if post.location %}
    <span class="project-card__location">
      <i class="fas fa-map-marker-alt" aria-hidden="true"></i>
      {{ post.location }}
    </span>
    {% endif %}
    <span class="project-card__status project-card__status--{{ status_key }}">{{ status_base }}{% if status_parts.size > 1 %} <span class="project-card__status-precision">({{ status_parts[1] | remove: ')' | strip }})</span>{% endif %}</span>
  </a>
  {% endfor %}
</div>
