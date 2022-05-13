---
title: Istruzioni online
permalink: index.html
layout: home
ms.openlocfilehash: 928f59a9cdc6a3f70d5ad651fb1b5a45b405cee8
ms.sourcegitcommit: 1117342052bce0bbd5a703bd1f763862b9129807
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/16/2022
ms.locfileid: "140682427"
---
# <a name="azure-data-fundamentals-exercises"></a>Esercizi per Concetti fondamentali sui dati di Azure

Usare i collegamenti seguenti per completare gli esercizi dei lab pratici per il corso Microsoft [DP-900 *Concetti fondamentali sui dati di Microsoft Azure*](https://docs.microsoft.com/learn/certifications/courses/dp-900t00).

Per completare gli esercizi, è necessaria una sottoscrizione a Microsoft Azure. Se non è stata fornita dal docente, è possibile iscriversi a una versione di valutazione gratuita in [https://azure.microsoft.com](https://azure.microsoft.com).

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| Modulo | Lab |
| --- | --- | 
{% for activity in labs  %}| {{ activity.lab.module }} | [{{ activity.lab.title }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
