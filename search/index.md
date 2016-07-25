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
  <div class="large-12 columns">
<form method="get" action="{{ site.url }}/search/" data-search-form class="simple-search">
      <div class="row collapse">
        <div class="large-10 columns">
  <input type="search" name="q" id="q" placeholder="What are you looking for?" data-search-input autofocus />
		 </div>
        <div class="large-2 columns">
  <span class="postfix"><input type="submit" value="Search" /></span>
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
