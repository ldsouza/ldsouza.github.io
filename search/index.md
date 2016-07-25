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
  
<div class="row collapse">     
  <div class="large-3 columns">
    <input type="text" placeholder="placeholder text" />
  </div>
  <div class="large-1 end columns">
	<input type="submit"><i class="fa fa-search"></i></input>
  </div>
</div>
<!-- Search form -->

<div class="row">
  <div class="ssmall-12 large-12 columns">
<form method="get" action="{{ site.url }}/search/" data-search-form class="simple-search">
      <div class="row collapse">
        <div class="small-10 large-10 columns">
  <input type="search" name="q" id="q" placeholder="What are you looking for?" data-search-input autofocus />
		 </div>
        <div class="small-2 large-2 columns">
<button type="submit"><i class="fa fa-thumbs-up"></i></button>
  </div>
  </div>
</form>
</div>
</div>
<!-- Search results placeholder -->
<h6 data-search-found>
  <span data-search-found-count></span> result(s) found for &ldquo;<span data-search-found-term></span>&rdquo;.
</h6>
<ul class="post-list" data-search-results></ul>

<!-- Search result template -->
<script type="text/x-template" id="search-result">
  <li><article>
    <a href="##Url##">##Title## <span class="excerpt">##Excerpt##</span></a>
  </article></li>
</script>
