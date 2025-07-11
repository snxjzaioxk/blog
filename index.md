---
layout: default
---

<header class="site-header">
  <div class="wrapper">
    <a class="site-title" href="{{ "/" | relative_url }}">{{ site.title | escape }}</a>
  </div>
</header>

<main class="page-content" aria-label="Content">
  <div class="wrapper">
    <div class="home">
      <h1>{{ site.title }}</h1> 

      <h2 class="post-list-heading">Posts</h2>
      <ul class="post-list">
        {% for post in site.posts %}
        <li>
          <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
          <h3>
            <a class="post-link" href="{{ post.url | relative_url }}">
              {{ post.title | escape }}
            </a>
          </h3>
          {% if site.show_excerpts %}
            {{ post.excerpt }}
          {% endif %}
        </li>
        {% endfor %}
      </ul>
    
      <p class="rss-subscribe">subscribe via <a href="{{ "/feed.xml" | relative_url }}">RSS</a></p>
    
    </div>
  </div>
</main>