---
layout: defaults/home-page
permalink: index.html
narrow: true
# title: Welcome to my blog
---
### Recent Posts
<hr>
{% for post in site.posts limit:3 %}
{% include components/post-card.html %}
{% endfor %}


