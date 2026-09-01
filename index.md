---
layout: default
title: Start
---

# Vibecoding Bootcamp – Lerntagebuch

Hier halte ich meine Lernerfolge und Erkenntnisse aus dem Vibecoding Bootcamp fest – ein Eintrag pro Tag.

## Einträge

<ul>
{% assign eintraege = site.tage | sort: "date" %}
{% for eintrag in eintraege %}
  <li>
    <a href="{{ eintrag.url | relative_url }}">{{ eintrag.title }}</a>
    {% if eintrag.date %} – {{ eintrag.date | date: "%d.%m.%Y" }}{% endif %}
  </li>
{% endfor %}
</ul>
