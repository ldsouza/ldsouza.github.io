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
  
  $("document").ready(function () {
  $("a[href$=.pdf]").after("<img src='http://placehold.it/16x16' align='absbottom' />")
  
  
});


$(document).foundation();

     // $("p[class]").css("border","3px solid red");
     // $("p[id^=para]").css("border","3px solid red");
     // $("p:contains(3)").css("border","3px solid red");
  // $("ul li:nth-child(2n)").css("border","3px solid red");
  // alert("there are " + $("p").length + " <p> elements");
  
  // var elems = $('li').get();
  // alert("there are " + elems.length + " <li> tags");
  // alert($('li').get(0));
  // $("ul").find("li.b").css("border","3px solid red");
 
  // var leftmargin=0;
 // var border = 0;
//  $("p").each(function() {
//    $(this).css("border", border + "px solid red");
 //   $(this).css("margin-left", leftmargin);
 //   border +=2;
  //  leftmargin += 10;
 // });


  
  <link type="text/css" rel="stylesheet" href="http://cdnjs.cloudflare.com/ajax/libs/foundicons/3.0.0/foundation-icons.css" />


<div class="row collapse">     
  <div class="large-3 columns">
    <input type="text" placeholder="placeholder text" />
  </div>
  <div class="large-1 end columns">
    <span class="postfix"><i class="fi-magnifying-glass"></i></span></input>
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
