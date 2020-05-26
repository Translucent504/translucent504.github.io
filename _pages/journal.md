---
title: "Journal"
layout: archive
permalink: /journal/
author_profile: false
---


<div class="entries-{{ page.entries_layout | default: 'list' }}">
          {% assign posts = site.tags.til | concat: site.tags.EPI %}
          
          {% for post in posts %}
            {% include archive-single.html type=page.entries_layout %}
          {% endfor %}
</div>
