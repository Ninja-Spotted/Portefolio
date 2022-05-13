---
title: "Title"
permalink: "/codeURLworkingmaybe/"
layout: default
---


{% for post in site.posts %}

    {{ post.url }}{{ post.title }}

{% endfor %}
