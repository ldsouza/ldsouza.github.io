---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: SQL Date Queries Cheatsheet
---
## A New Post

Enter text in [Markdown](http://daringfireball.net/projects/markdown/). Use the toolbar above, or click the **?** button for formatting help.

Current Date without Time
DATEADD(day, DATEDIFF(day, 0, GETDATE()), 0)
