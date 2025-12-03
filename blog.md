---
layout: default
role: nav
title: "Activity Log"
order: 6
---
Recent activity and progress updates on the program transformation initiative.

{% for post in site.posts %}
<article class="post-preview">
    <header>
        <h3>
            <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
        </h3>
        <p class="post-meta">
            <time datetime="{{ post.date | date_to_xmlschema }}">
                {{ post.date | date: "%B %d, %Y" }}
            </time>
            {% if post.categories %}
                <span class="post-category">
                    {% for category in post.categories %}
                        {{ category }}{% unless forloop.last %}, {% endunless %}
                    {% endfor %}
                </span>
            {% endif %}
        </p>
    </header>
    <div class="post-excerpt">
        {{ post.excerpt | strip_html | truncatewords: 30 }}
        <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Read more →</a>
    </div>
</article>
{% endfor %}
