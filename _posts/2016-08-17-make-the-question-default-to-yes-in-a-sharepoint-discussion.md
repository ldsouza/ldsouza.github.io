---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: Make the question default to yes in a SharePoint Discussion
---

In a SharePoint Discussion Board there is a default checkbox column named 'Question'. Unfortunately this is a sealed column and unlike other SharePoint columns, we are not able to change its properties and make it 'Yes' by default.

A way to solve this is using simple javascript. One the Add a Discussions page, edit the page and add a script editor webpart and past the following code snippet and save the changes. The next time you add a new discussion the 'Question' checkbox will default to 'Yes'. 

## Code Snippets

Syntax highlighting via Pygments

{% highlight css %}
<script type="text/javascript">
    function setCheckBox() {
        var theTDs = document.getElementsByTagName("input");       
        var i = 0;
        while (i < theTDs.length) {
            try {
                if (theTDs[i].type=="checkbox") {
                    theTDs[i].checked =true;
                }
            }
            catch (err) { }
            i = i + 1;
        }
    }
    _spBodyOnLoadFunctionNames.push("setCheckBox");
</script>
{% endhighlight %}

This solution was provided by Borislav Grgić and you can find it answered here.
