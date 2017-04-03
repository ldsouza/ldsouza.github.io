---
layout: post
category: SharePoint
tags:
  - SharePoint Online
  - Development
  - SharePoint
comments: false
title: CRUD Operations in SharePoint using the REST API (Part 2)
---
This is a blog post in the series 'CRUD Operations in SharePoint using the REST API'. In this series I will be performing **CRUD (Create, Read, Update, and Delete)** against SharePoint entities using the REST Representational State Transfer (REST) interface and jQuery Ajax.

In <a href="{{ site.github.url }}/sharepoint/crud-operations-in-sharepoint-using-the-rest-api">Part 1</a> of this series, I have shown you how to read and create list SharePoint List items using the REST API. 

The advantage of REST is that we can use http requests to retrieve or update SharePoint items without accessing any of the SharePoint libraries.

![Image]({{ site.url }}/images/blog/crud-sharepoint-rest/2.JPG)

In the previous post, I have created a custom SharePoint list named Customers and added the following columns to the list.

![Image]({{ site.url }}/images/blog/crud-sharepoint-rest/1.JPG)

### Update SharePoint List Items

![Image]({{ site.url }}/images/blog/crud-sharepoint-rest/5.JPG)

In this example, we will be updating a customer in the Customer List by constructing a RESTful HTTP request.

![Image]({{ site.url }}/images/blog/crud-sharepoint-rest/7.JPG)

**Javascript**
```javascript

// Update Operation

function Updateitem(id) {
    var itemProperties = {'Title':$("#cTitle").val(),'State': $("#cState").val(),'State': $("#txtState").val(),'Address':$("#cAddress").val(),'City': $("#cCity").val(),'Zip':$("#cZip").val(),'Gender':$("#cGender").val(),'Email':$("#cEmail").val()};
    var itemId = id; // Update Item Id here
    updateListItem(itemId, listName, url, itemProperties, function () {

		empty();

		Read();
    }, function () {
        alert("Ooops, an error occured. Please try again");
    });


function updateListItem(itemId, listName, siteUrl, itemProperties, success, failure) {
    var itemType = GetItemTypeForListName(listName);
 itemProperties["__metadata"] = { "type": itemType };
    getListItemWithId(itemId, listName, siteUrl, function (data) {
        $.ajax({
            url: data.__metadata.uri,
            type: "POST",
            contentType: "application/json;odata=verbose",
            data: JSON.stringify(itemProperties),
            headers: {
                "Accept": "application/json;odata=verbose",
                "X-RequestDigest": $("#__REQUESTDIGEST").val(),
                "X-HTTP-Method": "MERGE",
                "If-Match": data.__metadata.etag
            },
            success: function (data) {
                success(data);
            },
            error: function (data) {
                failure(data);
            }
        });
    }, function (data) {
        failure(data);
    });
}


function getListItemWithId(itemId, listName, siteurl, success, failure) {
    var url = siteurl + "/_api/web/lists/getbytitle('" + listName + "')/items?$select=Id,Title,State,Address,City,Zip,Gender,Email&$filter=Id eq " + itemId;
    $.ajax({
        url: url,
        method: "GET",
        headers: { "Accept": "application/json; odata=verbose" },
        success: function (data) {
            if (data.d.results.length == 1) {
                success(data.d.results[0]);
            }
            else {
                failure("Multiple results obtained for the specified Id value");
            }
        },
        error: function (data) {
            failure(data);
        }
    });
}
```

### Delete SharePoint List Items

![Image]({{ site.url }}/images/blog/crud-sharepoint-rest/8.JPG)

**Javascript**
```javascript

// Delete Operation
function Delete(id) {
    var itemId = id; // Update Item ID here
    deleteListItem(itemId, listName, url, function () {
		Read();
    }, function () {
        alert("Ooops, an error occured. Please try again");
    });
}

function deleteListItem(itemId, listName, siteUrl, success, failure) {
    getListItemWithId(itemId, listName, siteUrl, function (data) {
        $.ajax({
            url: data.__metadata.uri,
            type: "POST",
            headers: {
                "Accept": "application/json;odata=verbose",
                "X-Http-Method": "DELETE",
                "X-RequestDigest": $("#__REQUESTDIGEST").val(),
                "If-Match": data.__metadata.etag
            },
            success: function (data) {
                success(data);
            },
            error: function (data) {
                failure(data);
            }
        });
    },
   function (data) {
       failure(data);
   });
}

```

Using the REST API, you can build your own interfaces and forms to interact with SharePoint Data. There is some intricacy in getting a person field to work using the REST API. In a future blog post, I will cover using the client side people picker to accomplish this.
