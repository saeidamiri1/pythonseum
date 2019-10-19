---
layout: page
title: Posts relates
tagline: Python
---
{% include JB/setup %}


<ul class="posts">
    {% for post in site.posts %}
      <li>
        <h2>
          <span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url | prepend: site.baseurl}}">{{ post.title }}</a>
        </h2>
        <span class="post-meta">{{ post.author }}</span>
      </li>

      <img src="{{ site.baseurl }}/{{ post.image }}">

      <p>
      {{ post.excerpt }}
      <a class="btn btn-default" href="{{ post.url | prepend: site.baseurl }}">Continue reading...</a>
      </p>

    {% endfor %}

  </ul>

<div class="row-fluid">
  <div class="span12">
    <div class="pagination">
      <ul>
        {% if paginator.previous_page %}
          {% if paginator.previous_page == 1 %}
          <li><a href="/">Prev</a></li>
          {% else %}
          <li><a href="/page{{ paginator.previous_page }}">Prev</a></li>
          {% endif %}
        {% else %}
        <li><span class="disabled">Prev</span></li>
        {% endif %}
        {% if paginator.page == 1 %}
        <li><span class="active">1</span></li>
        {% else %}
        <li><a href="/">1</a></li>
        {% endif %}
        {% for count in (2..paginator.total_pages) %}
          {% if count == paginator.page %}
          <li><span class="active">{{ count }}</span></li>
          {% else %}
          <li><a href="/page{{ count }}">{{ count }}</a></li>
          {% endif %}
        {% endfor %}
        {% if paginator.next_page %}
        <li><a href="/page{{ paginator.next_page }}">Next</a></li>
        {% else %}
        <li><span class="disabled">Next</span></li>
        {% endif %}
      </ul>
    </div>
  </div>
</div>

-----
