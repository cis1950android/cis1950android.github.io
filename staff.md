---
layout: page
title: Staff
description: A listing of all the course staff members.
---

# Staff

The team you will be closely working with throughout the semester. Our #1 objective here is to serve you and ensure you have a good time. Let's keep that in mind :)

## Instructor

{% assign instructors = site.staffers | where: 'role', 'Instructor' %}
{% for staffer in instructors %}
{{ staffer }}
{% endfor %}

{% assign teaching_assistants = site.staffers | where: 'role', 'Teaching Assistant' %}
{% assign num_teaching_assistants = teaching_assistants | size %}
{% if num_teaching_assistants != 0 %}
## Teaching Assistant

{% for staffer in teaching_assistants %}
{{ staffer }}
{% endfor %}
{% endif %}
