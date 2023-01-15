---
title: "✌생각들"
layout: archive
permalink: categories/thought
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.Thought %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}