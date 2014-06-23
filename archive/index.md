---
title: Computational Communication
layout: page
---
{% capture jbcache %}
  <!--
  - Dynamically set liquid variables for working with URLs/paths
  -->
  {% if site.JB.setup.provider == "custom" %}
    {% include custom/setup %}
  {% else %}
    {% if site.safe and site.JB.BASE_PATH and site.JB.BASE_PATH != '' %}
      {% assign BASE_PATH = site.JB.BASE_PATH %}
      {% assign HOME_PATH = site.JB.BASE_PATH %}
    {% else %}
      {% assign BASE_PATH = nil %}
      {% assign HOME_PATH = "/" %}
    {% endif %}

    {% if site.JB.ASSET_PATH %}
      {% assign ASSET_PATH = site.JB.ASSET_PATH %}
    {% else %}
      {% capture ASSET_PATH %}{{ BASE_PATH }}/assets/themes/{{ page.theme.name }}{% endcapture %}
    {% endif %}  
  {% endif %}
{% endcapture %}{% assign jbcache = nil %}


<div class="page-header">
  <h1>All of My Posts <small>Everything I've Written!</small></h1>
</div>


<div class="row-fluid post-pagination">
  
{% for post in paginator.posts %}
  <div class="span6">
    <a href="{{ post.url }}">
      <h4>{{ post.title }}  <small>{{post.date | date_to_long_string }}</small></h4>
      <img src="{{ post.image }}" alt="{{ post.title }}" >
    </a>
  </div>
{% endfor %}


  <div class="span12">
    <div class="pagination">
      <ul>
      
      {% if paginator.previous_page %}
        <li class="prev"><a href="/posts/page{{ paginator.previous_page }}" title="Previous Page">&larr; Previous</a></li>
      {% else %}
        <li class="prev disabled"><a>&larr; Previous</a></li>
      {% endif %}
      
      <li{% if paginator.page == 1 %} class="active"{% endif %}><a href="/posts/">1</a></li>
      
      {% for count in (2..paginator.total_pages) %}
        {% if count == paginator.page %}
        <li class="active"><a href="/posts/page{{count}}">{{count}}</a></li>
        {% else %}
        <li><a href="/archive/page{{count}}">{{count}}</a></li>
        {% endif %}
      {% endfor %}
      
      {% if paginator.next_page %}
        <li class="next"><a href="/posts/page{{ paginator.next_page }}" title="Next Page">Next &rarr;</a></li>
      {% else %}
        <li class="next disabled"><a>Next &rarr;</a></li>
      {% endif %}
      </ul>
    </div>
  </div>
</div>

<ul class="listing">
{% for post in site.categories %}
    <li class="listing-item">
    <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
    <a href="{{ site.url }}{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
    
    <!-- 
    <p></p>
    {{ post.excerpt | remove: '<p>' | remove: '</p>' }} 
    -->
    </li>
{% endfor %}
</ul>
