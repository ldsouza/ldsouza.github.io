---
layout: post
title: "Implementing a Business Development/Sales Pipeline in SharePoint (Part 2)"
description: Part 2 of a Quick and Easy Solution to track your Sales Opportunities in SharePoint.
headline: 
modified: 2016-07-06
category: SharePoint
tags: [SharePoint, Office 365]
comments: true
mathjax: 
---

This is a blog post in the series “Implementing a Business Development/Sales Pipeline in SharePoint.”  In this series, I’ll show you how to implement a Pipline to manage and track opportunities.

In <a href="{{ site.github.url }}/sharepoint/sharepoint-sales-pipeline">Part 1</a> of this series, we have already setup a Custom list named Pipeline to track Opportunities and their status. We added the metadata columns associated to an opportunity and modified the default view. 


In this blog post, we will add custom views to easily group and view information in the Pipeline.

## Create Custom Views

## Opportunities Due in 90 Days
We will create a custom view to track the Opportunities whose 'Projected Close Date' is within the next 90 days. Select Create View from the List Tab and select start from an existing view 'All Items'.
![Image]({{ site.url }}/images/blog/pipeline2-create-view1.JPG)

In the Filter Section, apply the following filter. Since we would like to see all Opportunities that are going to be due in the next 90 days, set the 'Projected Close Date' <= [Today]+90.
![Image]({{ site.url }}/images/blog/pipeline2-create-view-due90.JPG)

![Image]({{ site.url }}/images/blog/pipeline2-create-view-due90-1.JPG)

---

## Opportunities Due in 30 Days
To create a view to track Opportunities whose 'Projected Close Date' is within the next 30 days, select create view and start from the existing view we just created 'Due 90 Days'.
![Image]({{ site.url }}/images/blog/pipeline2-create-view-copy.JPG) 

Modify the existing Filter from '[Today]+90' to '[Today]+30'.
![Image]({{ site.url }}/images/blog/pipeline2-create-view-due30.JPG)

---

## Track Number of Opportunities by Stage

To create a view to track Opportunities by stage, select create view and in the Group by Section, set First group by the Column to 'Stage'.
![Image]({{ site.url }}/images/blog/pipeline2-create-view-groupby.JPG) 

Now we have view to track Opportunities by Stage.
![Image]({{ site.url }}/images/blog/pipeline2-create-view-stage.JPG)

---

## Track my Opportunities

If you would like your Sales Staff to see the Opportunities they are responsible for, Create a new view and in the Filter Section, set 'Opportunity Owner' = [Me].
![Image]({{ site.url }}/images/blog/pipeline2-create-view-me.JPG)

In the next part of this series, I will cover a scenario where your 'Stage' may be a multiple choice and you would like to track the number of Opportunities in each Stage.

<a href="{{ site.url }}/sharepoint/sharepoint-sales-pipeline-3">Implementing a Business Development/Sales Pipeline in SharePoint (Part 3)</a>

Portland in shoreditch Vice, labore typewriter pariatur hoodie fap sartorial Austin. Pinterest literally occupy Schlitz forage. Odio ad blue bottle vinyl, 90's narwhal commodo bitters pour-over nostrud. Ugh est hashtag in, fingerstache adipisicing laboris esse Pinterest shabby chic Portland. Shoreditch bicycle rights anim, flexitarian laboris put a bird on it vinyl cupidatat narwhal. Hashtag artisan skateboard, flannel Bushwick nesciunt salvia aute fixie do plaid post-ironic dolor McSweeney's. Cliche pour-over chambray nulla four loko skateboard sapiente hashtag.

Vero laborum commodo occupy. Semiotics voluptate mumblecore pug. Cosby sweater ullamco quinoa ennui assumenda, sapiente occupy delectus lo-fi. Ea fashion axe Marfa cillum aliquip. Retro Bushwick keytar cliche. Before they sold out sustainable gastropub Marfa readymade, ethical Williamsburg skateboard brunch qui consectetur gentrify semiotics. Mustache cillum irony, fingerstache magna pour-over keffiyeh tousled selfies.

## Cupidatat 90's lo-fi authentic try-hard

In pug Portland incididunt mlkshk put a bird on it vinyl quinoa. Terry Richardson shabby chic +1, scenester Tonx excepteur tempor fugiat voluptate fingerstache aliquip nisi next level. Farm-to-table hashtag Truffaut, Odd Future ex meggings gentrify single-origin coffee try-hard 90's. 

* Sartorial hoodie 
* Labore viral forage
* Tote bag selvage 
* DIY exercitation et id ugh tumblr church-key

Incididunt umami sriracha, ethical fugiat VHS ex assumenda yr irure direct trade. Marfa Truffaut bicycle rights, kitsch placeat Etsy kogi asymmetrical. Beard locavore flexitarian, kitsch photo booth hoodie plaid ethical readymade leggings yr.

Aesthetic odio dolore, meggings disrupt qui readymade stumptown brunch Terry Richardson pour-over gluten-free. Banksy american apparel in selfies, biodiesel flexitarian organic meh wolf quinoa gentrify banjo kogi. Readymade tofu ex, scenester dolor umami fingerstache occaecat fashion axe Carles jean shorts minim. Keffiyeh fashion axe nisi Godard mlkshk dolore. Lomo you probably haven't heard of them eu non, Odd Future Truffaut pug keytar meggings McSweeney's Pinterest cred. Etsy literally aute esse, eu bicycle rights qui meggings fanny pack. Gentrify leggings pug flannel duis.

## Forage occaecat cardigan qui

Fashion axe hella gastropub lo-fi kogi 90's aliquip +1 veniam delectus tousled. Cred sriracha locavore gastropub kale chips, iPhone mollit sartorial. Anim dolore 8-bit, pork belly dolor photo booth aute flannel small batch. Dolor disrupt ennui, tattooed whatever salvia Banksy sartorial roof party selfies raw denim sint meh pour-over. Ennui eu cardigan sint, gentrify iPhone cornhole. 

> Whatever velit occaecat quis deserunt gastropub, leggings elit tousled roof party 3 wolf moon kogi pug blue bottle ea. Fashion axe shabby chic Austin quinoa pickled laborum bitters next level, disrupt deep v accusamus non fingerstache.

Tote bag asymmetrical elit sunt. Occaecat authentic Marfa, hella McSweeney's next level irure veniam master cleanse. Sed hoodie letterpress artisan wolf leggings, 3 wolf moon commodo ullamco. Anim occupy ea labore Terry Richardson. Tofu ex master cleanse in whatever pitchfork banh mi, occupy fugiat fanny pack Austin authentic. Magna fugiat 3 wolf moon, labore McSweeney's sustainable vero consectetur. Gluten-free disrupt enim, aesthetic fugiat jean shorts trust fund keffiyeh magna try-hard.

## Hoodie Duis

Actually salvia consectetur, hoodie duis lomo YOLO sunt sriracha. Aute pop-up brunch farm-to-table odio, salvia irure occaecat. Sriracha small batch literally skateboard. Echo Park nihil hoodie, aliquip forage artisan laboris. Trust fund reprehenderit nulla locavore. Stumptown raw denim kitsch, keffiyeh nulla twee dreamcatcher fanny pack ullamco 90's pop-up est culpa farm-to-table. Selfies 8-bit do pug odio.

### Thundercats Ho!

Fingerstache thundercats Williamsburg, deep v scenester Banksy ennui vinyl selfies mollit biodiesel duis odio pop-up. Banksy 3 wolf moon try-hard, sapiente enim stumptown deep v ad letterpress. Squid beard brunch, exercitation raw denim yr sint direct trade. Raw denim narwhal id, flannel DIY McSweeney's seitan. Letterpress artisan bespoke accusamus, meggings laboris consequat Truffaut qui in seitan. Sustainable cornhole Schlitz, twee Cosby sweater banh mi deep v forage letterpress flannel whatever keffiyeh. Sartorial cred irure, semiotics ethical sed blue bottle nihil letterpress.

Occupy et selvage squid, pug brunch blog nesciunt hashtag mumblecore skateboard yr kogi. Ugh small batch swag four loko. Fap post-ironic qui tote bag farm-to-table american apparel scenester keffiyeh vero, swag non pour-over gentrify authentic pitchfork. Schlitz scenester lo-fi voluptate, tote bag irony bicycle rights pariatur vero Vice freegan wayfarers exercitation nisi shoreditch. Chambray tofu vero sed. Street art swag literally leggings, Cosby sweater mixtape PBR lomo Banksy non in pitchfork ennui McSweeney's selfies. Odd Future Banksy non authentic.

Aliquip enim artisan dolor post-ironic. Pug tote bag Marfa, deserunt pour-over Portland wolf eu odio intelligentsia american apparel ugh ea. Sunt viral et, 3 wolf moon gastropub pug id. Id fashion axe est typewriter, mlkshk Portland art party aute brunch. Sint pork belly Cosby sweater, deep v mumblecore kitsch american apparel. Try-hard direct trade tumblr sint skateboard. Adipisicing bitters excepteur biodiesel, pickled gastropub aute veniam.