---
title: Work
layout: page
description: Some description.
permalink: "/work/"
---

<style>

.post-content .pt130{padding-top:130px;}


@media (max-width: 620px) {
    .content{height:unset;}

}
@media (max-width: 1500px) {
    .content{height:unset;}

}
</style>

<!-- <img class="img-rounded" src="/assets/img/uploads/profile.png" alt="Thiago Rossener" width="200"> -->
<p class="pt130"></p>

<!-- Posts -->
<section id="grid" class="row flex-grid">
    {% for post in posts offset: offset %}
        <article class="box-item">
            <span class="category">
                <a href="{{ site.baseurl }}/{{ site.categories_folder | default: 'category' }}/{{ post.category }}">
                    <span>{{ post.category }}</span>
                </a>
            </span>
            <div class="box-body">
                <a class="cover" href="{{ post.url | prepend: site.baseurl }}">
                    {% include loader.html %}
                    {% if post.optimized_image %}
                        <img src="/assets/img/placeholder.png" width="100%" data-url="{{ post.optimized_image }}" class="preload">
                        <noscript>
                            <img src="{{ post.optimized_image }}" width="100%">
                        </noscript>
                    {% elsif post.image %}
                        <img src="/assets/img/placeholder.png" width="100%" data-url="{{ post.image }}" class="preload">
                        <noscript>
                            <img src="{{ post.image }}" width="100%">
                        </noscript>
                    {% else %}
                        <img src="/assets/img/placeholder.png" width="100%" data-url="/assets/img/off.jpg" class="preload">
                        <noscript>
                            <img src="/assets/img/off.jpg" width="100%">
                        </noscript>
                    {% endif %}
                    {% include new-post-tag.html date=post.date %}
                    {% include read-icon.html %}
                </a>
                <div class="box-info">
                    <time datetime="{{ post.date | date_to_xmlschema }}" class="date">
                        {% include date.html date=post.date %}
                    </time>
                    <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">
                        <h2 class="post-title">
                            {{ post.title }}
                        </h2>
                    </a>
                    <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">
                        <p class="description">{{ post.description }}</p>
                    </a>
                    <div class="tags">
                        {% for tag in post.tags %}
                            {% if tag != "" %}
                                <a href="{{ site.baseurl}}/tags/#{{tag | slugify }}">#{{ tag }}</a>
                            {% endif %}
                        {% endfor %}
                    </div>
                </div>
            </div>
        </article>
    {% endfor %}
</section>
