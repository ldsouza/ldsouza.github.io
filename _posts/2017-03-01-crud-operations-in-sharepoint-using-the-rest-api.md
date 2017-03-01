---
layout: post
published: false
mathjax: false
featured: false
comments: false
title: CRUD Operations in SharePoint using the REST API
---
## A New Post

Enter text in [Markdown](http://daringfireball.net/projects/markdown/). Use the toolbar above, or click the **?** button for formatting help.

var listName = "Customers";
var url = _spPageContextInfo.webAbsoluteUrl;
function Read() { 
    getListItems(listName, url, function (data) {
        var items = data.d.results;
 var output;
 output = "<table class='table'><tr><th>Customer Name</th><th>Gender</th><th>Email</th><th>Address</th><th>City</th><th>State</th><th>Zip</th></tr>";
        // Add all the new items
        for (var i = 0; i < items.length; i++) {
            output = output + "<tr><td>" + items[i].Title + "</td><td>" + items[i].Gender +"</td><td>" + items[i].Email +"</td><td>" + items[i].Address +"</td><td>" + items[i].City +"</td><td>" + items[i].State +"</td><td>" + items[i].Zip +"</td></tr>";
       
        }
    $("#divList").html(output);

    }, function (data) {
        alert("Ooops, an error occured. Please try again");
    });
}
 
// READ operation
// listName: The name of the list you want to get items from
// siteurl: The url of the site that the list is in. 
// success: The function to execute if the call is sucesfull
// failure: The function to execute if the call fails
function getListItems(listName, siteurl, success, failure) {
var userId = _spPageContextInfo.userId;
var restURL = siteurl + "/_api/web/lists/getbytitle('" + listName + "')/items";
    $.ajax({
        url: restURL,
        method: "GET",
        headers: { "Accept": "application/json; odata=verbose" },
        success: function (data) {
            success(data);
        },
        error: function (data) {
            failure(data);
        }
    });
}
