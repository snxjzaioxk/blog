# {{ site.title }}

**{{ site.url }}**

## Posts

{% for post in site.posts %}
{{ post.date | date: "%b %d, %Y" }}  
**{{ post.title }}**
{% endfor %}

subscribe via RSS