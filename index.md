---
title: Istruzioni online
permalink: index.html
layout: home
---

# <a name="azure-data-fundamentals-exercises"></a>Esercizi per Concetti fondamentali sui dati di Azure

Questi esercizi pratici sono progettati a supporto del contenuto di training in [Microsoft Learn](https://docs.microsoft.com/training/).

Per completare questi esercizi, sarà necessaria una sottoscrizione di Microsoft Azure con autorizzazioni amministrative. È possibile iscriversi per una versione di valutazione gratuita all’indirizzo [https://azure.microsoft.com](https://azure.microsoft.com).

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| Esercizio |
| --- |
{% for activity in labs  %}| [{{ activity.lab.title }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
