---

icon: fas fa-info-circle
order: 4
hidden: true 
---
{% for tab in site.tabs %}
- {{ tab.title }} — hidden: {{ tab.hidden }}
{% endfor %}

> Add Markdown syntax content to file `_tabs/about.md`{: .filepath } and it will show up on this page.
{: .prompt-tip }
