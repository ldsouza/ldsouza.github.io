---
layout: post
published: false
mathjax: false
featured: false
comments: false
title: CRUD Operations in SharePoint using the REST API
---
## A New Post

This is part 1 of the series in which we will be performing CRUD (Create, Read, Update, and Delete) against SharePoint entities using the REST Representational State Transfer (REST) interface.

The advantage of REST is that we can use http requests to retrieve or update SharePoint items without accessing any of the SharePoint libraries.

Read SharePoint List Items

In this example, we will be reading a Customer List by making a GET Request.
Set the name of the list you want to read from. In this instance our list name is Customers.

The Javascript
```javascript

// READ operation
var listName = "Customers";
var url = _spPageContextInfo.webAbsoluteUrl;
function Readlist() { 
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
 
function getListItems(listName, siteurl, success, failure) {
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
```

```javascript
function add()
{

	var itemProperties = {'Title':$("#cTitle").val(),'Gender': $("#cGender").val(),'Email': $("#cEmail").val(),'Address': $("#cAddress").val(),'City': $("#cCity").val(),'State': $("#cState").val(),'Zip': $("#cZip").val()};
    
	createListItem(url,listName,itemProperties,function () {

		empty();
		
				
    }, function () {
        alert("Ooops, an error occured. Please try again");
    });
}

//Create operation

function createListItem(siteUrl,listName, itemProperties, success, failure) {
var itemType = GetItemTypeForListName(listName);
    itemProperties["__metadata"] = { "type": itemType };

    $.ajax({
        url: siteUrl + "/_api/web/lists/getbytitle('" + listName + "')/items",
        type: "POST",
        contentType: "application/json;odata=verbose",
        data: JSON.stringify(itemProperties),
        headers: {
            "Accept": "application/json;odata=verbose",
            "X-RequestDigest": $("#__REQUESTDIGEST").val()
        },
        success: function (data) {
            success(data.d);
        },
        error: function (data) {
            failure(data);
        }
    });
}


function empty() {
    $("#cTitle").val("");
	$("#cState").val("");
	$("#cAddress").val("");
    $("#cCity").val("");
	$("#cZip").val("");
	$("#cEmail").val("");
    $("#cGender").val("");
   
}
```