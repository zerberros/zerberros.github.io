---
layout: home
title: index
---


<ul>
  {% for post in site.categories.blog %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {{ post.resumen }}
   <br/><br/>

  {% endfor %}
</ul>
