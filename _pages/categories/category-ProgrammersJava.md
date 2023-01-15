{% assign posts = site.categories.BojJava %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}