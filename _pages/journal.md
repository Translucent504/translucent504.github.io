---
title: "Journal"
layout: default
permalink: /journal/
author_profile: false
---

{% for tag in site.tags.til %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}

<div class="entries-{{ page.entries_layout | default: 'list' }}">
          {% for post in site.tags.til %}
            {% include archive-single.html type=page.entries_layout %}
          {% endfor %}
</div>
