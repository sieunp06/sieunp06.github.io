---
title: "✅What Todo"
layout: archive
permalink: categories/todo
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.Todo %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}