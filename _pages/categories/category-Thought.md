{% assign posts = site.categories.Thought %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}