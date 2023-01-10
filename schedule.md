---
layout: page
title: Schedule
nav_order: 3
description: Listing of course modules and topics.
---

# **Weekly Schedule**

{% for module in site.modules %}
{{ module }}
{% endfor %}
