---
title: "blog"
layout: archive
permalink: Category/Git
---


{% assign posts = site.categories.Category_Git %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}