---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

  You can also find my articles on <a href="https://scholar.google.ch/citations?user=CSHe53oAAAAJ&hl=en&oi=ao">my Google Scholar profile</a>.

{% include base_path %}

{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}
