---
layout: page
permalink: /about/index.html
title: Hossain Mohd Faysal
tags: [Hossain, Mohd, Faysal, hmfaysal]
imagefeature: fourseasons.jpg
chart: true
---


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

*[ESE]: Electrical and Systems Engineering
*[SEAS]: School of Engineering and Applied Science
*[MIT]: Massachusetts Institute of Technology
*[EECS]: Electrical and Computer Engineering
*[UPENN]: University of Pennsylvania

<figure>
	<img src="{{ site.url }}/images/Hossain-Mohd-Faysal.jpg" alt="Hossain Mohammad Faysal">
	<figcaption>At Bates Linear Accelerator Center</figcaption>
</figure>

I was born and brought up in Doha. Yes, its a desert peninsula, yes we have camels and falcons and all the other Middle Eastern traits/stereotypes you can think of.

<figure class="third">
	<a href="{{ site.url }}/images/about/1.jpg"><img src="{{ site.url }}/images/about/1-001.jpg"></a>
	<a href="{{ site.url }}/images/about/2.jpg"><img src="{{ site.url }}/images/about/2-001.jpg"></a>
	<a href="{{ site.url }}/images/about/3.jpg"><img src="{{ site.url }}/images/about/3-001.jpg"></a>
</figure>
<figure class="half">
	<a href="{{ site.url }}/images/about/4.jpg"><img src="{{ site.url }}/images/about/4-001.jpg"></a>
	<a href="{{ site.url }}/images/about/5.jpg"><img src="{{ site.url }}/images/about/5-001.jpg"></a>
</figure>
<figure class="third">
	<a href="{{ site.url }}/images/about/6.jpg"><img src="{{ site.url }}/images/about/6-001.jpg"></a>
	<a href="{{ site.url }}/images/about/7.jpg"><img src="{{ site.url }}/images/about/7-001.jpg"></a>
	<a href="{{ site.url }}/images/about/8.jpg"><img src="{{ site.url }}/images/about/8-001.jpg"></a>
	<figcaption>Doha at its full glory.</figcaption>
</figure>

At some point in the not-terribly-distant future, I hope to found a self-sustaining collective of clever people, for fun, profit(?), and the promotion of human life in the universe. This might wind up in Qatar, Bangladesh, Scandinavia, the Massachusetts Bay Area, the SF Bay Area, Japan, Germany, or the dustbin of overly idealistic plans. (Yes, I have a special bin for overly idealistic plans. In my district they can't be recycled with residential mixed paper.) The most challenging aspect of this concept is to curtail unproductive competition with other people who will inevitably have the same idea. (Some sort of cooperative federation...) I'm presently looking for people who might be interested in being a part of such an organization.

Anyways, for now I'm just working toward changing the face of Electrical Engineering forever. Not that I necessarily expect to succeed, but it's something to strive for, and it's a fun problem to work on.


Entrepreneur  
Designer  
***Engineer***  
Inventor  

I
make
stuff.


*Beautiful, practical, meaningful stuff.*


I make what I love.

*I love what I do.*


But over the years, I noticed that somehow, along the way, software designed to help us be creative, actually made us less creative. That's because we believe our best ideas emerge when we use pencils and paper.
So I set out to build tools that work the way I do.


Tools for the creative space — the 53 centimeters that magically link head, heart, and hand. Tools as simple as pencil and paper. Tools so essential, I  really can't imagine work without them.


For
the makers,  
the creators,  
the discoverers,  
the original thinkers,  
***This is the space to create.***