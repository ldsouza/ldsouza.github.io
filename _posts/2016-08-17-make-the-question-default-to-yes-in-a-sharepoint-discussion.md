---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: Change the Question default checkbox in a SharePoint Discussion
categories: 'SharePoint'
tags: 
- SharePoint
- Office 365
---

In a SharePoint Discussion Board there is a default checkbox column named 'Question'. Unfortunately this is a sealed column and unlike other SharePoint columns, we are not able to change its properties and make it 'Yes' by default.

![Image]({{ site.url }}/images/blog/sharepoint-discussion-default.JPG)

A way to solve this is using simple javascript. One the Add a Discussions page, edit the page and add a script editor webpart and past the following code snippet and save the changes. The next time you add a new discussion the 'Question' checkbox will default to 'Yes'. 

## Code Snippets

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

This solution was provided by Borislav Grgić and you can find it on <a href="https://social.technet.microsoft.com/Forums/office/en-US/8746b540-50b7-4280-965f-e32c44ccd476/community-site-changing-the-asking-a-question-checkbox-default-to-checked?forum=sharepointgeneral">Technet</a>.
