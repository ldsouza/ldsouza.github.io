---
layout: post
category: SharePoint
tags:
  - SharePoint Online
  - Development
  - SharePoint
comments: false
title: CRUD Operations in SharePoint using the REST API
---
This is a blog post in the series 'CRUD Operations in SharePoint using the REST API'. In this series I will be performing **CRUD (Create, Read, Update, and Delete)** against SharePoint entities using the REST Representational State Transfer (REST) interface and jQuery Ajax.

![Image]({{ site.url }}/images/blog/crud-sharepoint-rest/2.JPG)

The advantage of REST is that we can use http requests to retrieve or update SharePoint items without accessing any of the SharePoint libraries.

Create a custom SharePoint list named Customers and add the following columns to the list.

![Image]({{ site.url }}/images/blog/crud-sharepoint-rest/1.JPG)

### Read SharePoint List Items

![Image]({{ site.url }}/images/blog/crud-sharepoint-rest/3.JPG)

In this example, we will be reading a Customer List by making a GET Request.
Set the name of the list you want to read from. In this instance our list name is Customers.

**Javascript**
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
    $("#divSPList").html(output);

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

**HTML**
```javascript
<body onload="Readlist()">
  <div id="divSPList"></div>
</body>
  ```

### Create SharePoint List Items

![Image]({{ site.url }}/images/blog/crud-sharepoint-rest/4.JPG)

In this example, we will be adding new customers to the Customer List by constructing a RESTful HTTP request, but this time we will be using a POST request.

**Javascript**
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

**HTML**
```javascript
<div class="col-sm-10">
<form class="form-horizontal">

<legend>Add Customer</legend>
      <label style="display:none;" id="cId"></label>
<div class="form-group">
      <label control-label" for="textinput">Name</label>
      <input name="cTitle" id="cTitle" type="text" class="form-control" input-sm" placeholder="Enter Name">
</div>


 <div class="form-group">
     <label control-label" for="textinput">Gender</label>
    <select name="cGender" id="cGender" type="text" class="form-control" input-sm" placeholder="Enter Gender">
        <option>Male</option>
        <option>Female</option>
      </select>
 </div>

 <div class="form-group">
     <label control-label" for="textinput">Email</label>  
      <input name="cEmail" id="cEmail" type="text" class="form-control" input-sm" placeholder="Enter Email">
 </div>

 <div class="form-group">
     <label control-label" for="textinput">Address</label>  
      <input name="cAddress" id="cAddress" type="text" class="form-control" input-sm" placeholder="Enter Address">
 </div>

 <div class="form-group">
     <label control-label" for="textinput">City</label>  
      <input name="cCity" id="cCity" type="text" class="form-control" input-sm" placeholder="Enter City">
 </div>

 <div class="form-group">
     <label control-label" for="textinput">State</label>
   <select name="cState" id="cState" type="text" class="form-control" input-sm" placeholder="Enter State">
        <option>DC</option>
        <option>VA</option>
        <option>MD</option>
      </select>
  </div>

 <div class="form-group">
     <label control-label" for="textinput">Zip</label>  
      <input name="cZip" id="cZip" type="text" class="form-control" input-sm" placeholder="Enter Zip">
 </div>


 <div class="form-group">
    <button onclick="operation('add')" type="button" id="btnAddSubmit" class="btn btn-success" value="Add">Save </button>
    <button id="button2id" name="button2id" class="btn btn-danger">Clear</button>
</div>

</form>
</div>
```

Using the REST API, you can build your own interfaces and forms to interact with SharePoint Data.  In the next part of this blog post series, I will cover the Update and Delete operations you can perform on SharePoint List Items using REST.
