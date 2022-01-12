---
title: test
layout: page
description: Some description.
permalink: "/test/"
---

<style>

.post-content .pt130{padding-top:130px;}
.home {
  @include mainFont(400);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  padding-top: rem(80px);

  @include media(">=sm") {
    padding-top: rem(100px);
  }

  &.no-padding {
    padding-top: 0;
  }
}

.row {
  @include center(100%);
  margin: 0px rem($rowMargin);
}

.flex-grid {
  display: flex;
  flex-flow: row wrap;
}

.title-category {
  font-size: rem(32px);
  margin: 0 0 rem(40px);
  padding: 0 rem(23px);
  text-transform: lowercase;
  color: #fff;
}

.box-item {
  flex: 1 0 $itemMinWidth;
  margin: 0 0 rem(30px);
  display: inline-block;
  min-height: rem(285px);
  transition: all 0.3s;
  position: relative;
  z-index: 1;

  @include media(">=sm") {
    margin: 0 rem($itemMargin) rem(30px);
  }

  // Note 1: This complex calc right here is what makes the leftover box items
  // have the same width than their siblings.
  @for $n from 2 through $maxItemsPerRow {
    $resolution: (2 * $rowMargin) + ($n * $itemMinWidth);
    @include media(">=#{$resolution}") {
      max-width: calc(100%/#{$n} - #{$itemMargin * 2});
    }
  }

  // Note 2: This sets the maximum number of box items per row.
  @include media(">=#{(2 * $rowMargin) + ($maxItemsPerRow * $itemMinWidth)}") {
    flex: 1 0 calc(100%/#{$maxItemsPerRow} - #{$itemMargin * 2});
  }

  &:hover {
    z-index: 2;
    transform: scale(1.1);

    img {
      -webkit-filter: grayscale(100%);
      filter: grayscale(100%);
      transform: scale(1.05);
    }

    .box-body {
      time,
      p {
        color: $accentDark;
      }

      .cover {
        .new-post-tag {
          background-color: #000;
        }

        .read-icon {
          opacity: 1;
        }
      }
    }
  }

  a {
    text-decoration: none;
    display: block;
  }

  .category {
    display: block;
    height: rem(36px);
    line-height: rem(36px);
    text-transform: uppercase;
    font-weight: bold;
    font-size: rem(18px);
    padding: 0 rem(15px);

    a {
      color: $accentDark;
    }
  }

  .box-body {
    img {
      width: 100%;
      height: auto;
      margin: 0 auto;
      transition: all 0.2s ease-in-out;
    }

    time {
      font-weight: 300;
      font-size: rem(16px);
      color: darken($lightGray, 50%);
      pointer-events: none;
    }

    h2 {
      margin: rem(10px) 0;
      font-size: rem(24px);
      @include mainFont(800);
      color: $accentDark;
      line-height: rem(30px);
    }

    p {
      margin: 0 0 rem(30px);
      color: darken($lightGray, 20%);
      font-size: rem(17px);
      line-height: rem(26px);
    }

    .tags a {
      height: rem(30px);
      line-height: rem(26px);
      color: $accentDark;
      padding: 0 rem(10px);
      border: 1px solid $accentDark;
      border-radius: 15px;
      display: inline-block;
      margin: 0 rem(10px) rem(10px) 0;
      z-index: 50;

      &:hover {
        color: $primaryDark;
        background: $accentDark;
        border-color: $accentDark;
      }
    }

    .cover {
      position: relative;
      display: block;

      .loader {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate3d(-50%, -50%, 0);
        color: $themeColor;
        z-index: 1;
      }

      img {
        position: relative;
        z-index: 2;
      }

      .new-post-tag {
        text-transform: uppercase;
        display: inline-block;
        background: $themeColor;
        color: #fff;
        font-size: rem(13px);
        font-weight: 700;
        line-height: rem(24px);
        padding: 0 rem(8px);
        position: absolute;
        bottom: rem(8px);
        left: 0;
        z-index: 3;
      }

      .read-icon {
        opacity: 0;
        background-color: rgba(0, 0, 0, 0.7);
        display: flex;
        align-items: center;
        justify-content: center;
        content: "";
        width: rem(80px);
        height: rem(80px);
        border-radius: 40px;
        position: absolute;
        top: 50%;
        left: 50%;
        margin-top: rem(-40px);
        margin-left: rem(-40px);
        border: 2px solid #fff;
        color: $themeColor;
        z-index: 4;

        svg {
          width: rem(48px);
        }
      }
    }
  }

  .box-info {
    padding: rem(15px);
  }
}
.description{word-wrap: break-word; word-break: keep-all; font-size: 1rem;}

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
<main class="home {% if site.show_hero and paginator == nil or paginator.page == 1 %}no-padding{% endif %}">
    
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
<!-- Pagination -->
{% if site.paginate %}
    {% include pagination-home.html %}
{% endif %}
</main>


<script type="application/ld+json">
{
  "@context": "http://schema.org",
  "@type": "WebPage",
  "mainEntity": {
    "@type": "Blog",
    "name": "{{ site.name }}",
    "headline": "{{ site.title }}",
    "description": "{{ site.description }}",
    "url": "{{ site.url }}{{site.baseurl}}/",
    "inLanguage": "{{ site.language }}",
    "isFamilyFriendly": "true",
    "creator": {
        "@type": "Organization",
        "name": "{{ site.name }}",
        "url": "{{ site.url }}{{site.baseurl}}/",
        "sameAs": [
            {{ social_urls | split: "," | join: "," }}
        ]
    },
    "mainEntity": {
        "@type": "ItemList",
        "itemListElement": [
        {% assign limit = 8 %}
        {% for post in posts limit: limit %}
            {% assign author = site.authors | where: "name", post.author | first %}
            {
                "@type": "BlogPosting",
                "name": "{{ post.title }}",
                "headline": "{{ post.subtitle }}",
                "description": "{{ post.description }}",
                "image": "{{ post.image }}",
                "url": "{{ post.url | prepend: site.baseurl | prepend: site.url }}",
                "inLanguage": "{{ site.language }}",
                "dateCreated": "{{ post.date | date: '%Y-%m-%d/' }}",
                "datePublished": "{{ post.date | date: '%Y-%m-%d/' }}",
                "dateModified": "{{ post.date | date: '%Y-%m-%d/' }}",
                "author": {
                    "@type": "Person",
                    "name": "{{ author.display_name }}",
                    "url": "{{ author.url | prepend: site.baseurl | prepend: site.url }}"
                },
                "publisher": {
                    "@type": "Organization",
                    "name": "{{ site.name }}",
                    "url": "{{ site.url }}{{site.baseurl}}/",
                    "logo": {
                        "@type": "ImageObject",
                        "url": "{{ site.url }}{{site.baseurl}}/assets/img/blog-image.png",
                        "width": "600",
                        "height": "315"
                    }
                },
                "mainEntityOfPage": "True",
                "genre": "{{ post.category | capitalize }}",
		        "articleSection": "{{ post.category | capitalize }}",
                "keywords": [{{ post.tags | join: '","' | append: '"' | prepend: '"' }}]
            }{% if forloop.last == false  %},{% endif %}
        {% endfor %}
        ]
    }
  }
}
</script>
