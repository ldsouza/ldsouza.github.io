---
layout: page
title: "Search"
date: 
modified:
excerpt:
image:
  feature:
search_omit: true
sitemap: false
---

<!-- Search form -->

<div class="row">
  <div class="small-10 large-centered columns">
<form method="get" action="{{ site.url }}/search/" data-search-form class="simple-search">
   <div class="small-11 columns">
  <input style="height: 50px; border-width:0px; position: absolute;" type="search" name="q" id="q" placeholder="What are you looking for?" data-search-input autofocus />
  </div>
 <div class="small-1 columns"> 
<button style="height: 50px; background-color: #FEC110;" type="submit"><i class="fa fa-search"></i></button>
  </div>
</form>
</div>
</div>
<!-- Search results placeholder -->
<h6 data-search-found>
  <span data-search-found-count></span> result(s) found for &ldquo;<span data-search-found-term></span>&rdquo;.
</h6>
<ul style="list-style: none;" data-search-results></ul>

<!-- Search result template -->
<script type="text/x-template" id="search-result">
  <li style="padding: 5px 0 2px 0; border-bottom: 1px solid rgba(0,0,0,0.1); font-size: 1.125rem; line-height:1.33333;"><article>
    <a style="color:#FEC110;"href="##Url##">##Title##</a><br>
	<a style="color:#000; font-size: .875rem"href="##Url##">##Excerpt##</a>
  </article></li>
</script>
