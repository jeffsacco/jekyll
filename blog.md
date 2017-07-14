---
layout: page
title: Blog items
permalink: /blog/
---

<section class="site-section">

    <div class="wrapper">

        <ul class="post-list">
        
        {% for post in site.categories['blog'] %}
          
          <li class="postt">
          <ul class="icon-tags">
            {% for tag in post.tags %}
              <li><img src="/images/icon-{{tag}}.png" alt="{{tag}}"></li>
            {% endfor %}
          </ul>
            <h2><a href="{{post.url | prepend: site.baseurl }}">{{post.title}}</a></h2>
            <p>{{post.content | strip_html | strip_newlines | truncate:200 }}</p>
            <p class="post-read-more-link"><a href="{{post.url | prepend: site.baseurl}}">Read more</a></p>

          </li>
        {% endfor %}
        </ul>
      
    </div>
    
  </section>