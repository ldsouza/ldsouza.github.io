---
layout: page
permalink: /about/index.html
title: Laurel Dsouza
tags: [ldsouza]
imagefeature: fourseasons.jpg
chart: true
---
<figure>
  <img src="{{ site.url }}/images/laurel-dsouza.jpg" alt="Laurel Dsouza">
  <figcaption>Laurel Dsouza</figcaption>
</figure>

{% assign total_words = 0 %}
{% assign total_readtime = 0 %}
{% assign featuredcount = 0 %}
{% assign statuscount = 0 %}

{% for post in site.posts %}
    {% assign post_words = post.content | strip_html | number_of_words %}
    {% assign readtime = post_words | append: '.0' | divided_by:200 %}
    {% assign total_words = total_words | plus: post_words %}
    {% assign total_readtime = total_readtime | plus: readtime %}
    {% if post.featured %}
    {% assign featuredcount = featuredcount | plus: 1 %}
    {% endif %}
{% endfor %}


My name is **Laurel Dsouza**, and this is my blog. I am a Professional BI & Cloud Solutions consultant based out of Virginia, USA.

I graduated with a Masters Degree in Telecommunications from George Mason University and have been working on Microsoft Technologies since 2008. My journey with SharePoint and SQL began as a administrator and from there I got more involved in design and building solutions as a developer. I strive to build innovative business solutions for my clients using new technologies and the power of cloud computing.

I spend my free time playing the guitar, reading, blogging and building websites. I love swimming and playing sports like soccer, tennis and basketball. If you would like to connect with me, my social media profile links are at the bottom.

Keep an eye on my blog to get updated on real world solutions, tutorials and tips on BI, SharePoint, Office 365, Azure and related technologies.


