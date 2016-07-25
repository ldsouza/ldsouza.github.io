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
  <div class="small-12 columns">
<form method="get" action="{{ site.url }}/search/" data-search-form class="simple-search">
      <div class="row collapse">
        <div class="small-11 columns">
  <input type="search" name="q" id="q" placeholder="What are you looking for?" data-search-input autofocus />
		 </div>
        <div class="small-1 columns">
<button style="height: 52px; background-color: #FEC110;" type="submit"><i class="fa fa-search"></i></button>
  </div>
  </div>
</form>
</div>
</div>
<!-- Search results placeholder -->
<h6 data-search-found>
  <span data-search-found-count></span> result(s) found for &ldquo;<span data-search-found-term></span>&rdquo;.
</h6>
<ul data-search-results></ul>

<!-- Search result template -->
<script type="text/x-template" id="search-result">
  <li><article>
    <a style="color:#FEC110;"href="##Url##">##Title##</a><br>
	<a style="color:#000;"href="##Url##">##Excerpt##</a>
  </article></li>
</script>
