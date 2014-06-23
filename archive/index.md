---
title: Computational Communication
layout: page
---



<ul class="listing">
{% for post in site.categories.blog %}
    <li class="listing-item">
    <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
    <a href="{{ site.url }}{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
    <p></p>
    {{ post.excerpt | remove: '<p>' | remove: '</p>' }}
    </li>
{% endfor %}
</ul>


{% for post in paginator.posts %}
  <h1><a href="{{ post.url }}">{{ post.title }}</a></h1>
  <p class="author">
    <span class="date">{{ post.date }}</span>
  </p>
  <div class="content">
    {{ post.content }}
  </div>
{% endfor %}

<div class="pagination">
  {% if paginator.previous_page %}
    <a href="/page{{ paginator.previous_page }}" class="previous">Previous</a>
  {% else %}
    <span class="previous">Previous</span>
  {% endif %}
  <span class="page_number ">Page: {{ paginator.page }} of {{ paginator.total_pages }}</span>
  {% if paginator.next_page %}
    <a href="/page{{ paginator.next_page }}" class="next">Next</a>
  {% else %}
    <span class="next ">Next</span>
  {% endif %}
</div>

{% if paginator.total_pages != 1  %}
<div id="pagination" class="pagination">
    <ul class="pages fix_height">
        {% if paginator.page == 1  %}
        <li class="current-page">
            <span>1</span>
            {% else  %}
        <li class="page">
            <a href="{{ pager_url  }}/">1</a>
            {% endif  %}
        </li>
        {% for count in (2..paginator.total_pages)  %}

        {% if count == paginator.page  %}
        <li class="page current-page">
            <span>{{ count  }}</span>
            {% else  %}
        <li class="page">
            <a href="{{ pager_url  }}/page{{ count  }}/">{{ count  }}</a>
            {% endif  %}
        </li>
        {% endfor  %}
        <li class="page last_page">
            <a href="{{ pager_url  }}/page{{ paginator.total_pages  }}/">Last</a>
        </li>
    </ul>
</div>
{% endif   %}
