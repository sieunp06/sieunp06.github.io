---
title: "✌나 놀고 왔다"
layout: archive
permalink: categories/playing
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.Playing %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}