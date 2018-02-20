---
layout: proyectos
title: proyectos
---


  {% for proyect in site.categories.proyectos %}

## {{ proyect.title }}

![ {{  proyect.title}}  ]( {{ proyect.foto }} )

{{  proyect.resumen  }}


{% if proyect.enlace %}
[ archivos fuente ]( {{  proyect.enlace  }} )

{% endif %}
-----

  {% endfor %}
