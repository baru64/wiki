<!-- TITLE: Portal API -->
<!-- SUBTITLE: A quick summary of Portal API -->

# The Portal API backend
The portal API backend is written in Java. The design described here is also reflected in the code

The backend API is under <serverURL>/5ginfireportal/services/api/repo/* and <serverURL>/5ginfireportal/services/api/repo/repo/admin/* for authorized requests. For example, since our portal will be under https://portal.5ginfire.eu you can request towards: https://portal.5ginfire.eu/5ginfireportal/services/api/repo/* 
The API, Produces("application/json") and Consumes("application/json") except some POSTs that Consume("multipart/form-data") All requests should be to the /repo of the webservice. 

> The API endpoint is at:
https://portal.5ginfire.eu/5ginfireportal/services/api/repo/*
A complete API documentation can be found at:
https://5ginfire.github.io/eu.5ginfire.portal.api/doc/html2-client/ 
The API has an OpenAPI [^1] specification under: 
https://portal.5ginfire.eu/5ginfireportal/services/api/swagger.json


There are requests that are public. For example, get all Categories:


```sh
curl -v  https://portal.5ginfire.eu/5ginfireportal/services/api/repo/categories
```


response:


```json
[
  {
    "id": 1,
    "name": "None",
    "appscount": 0,
    "vxFscount": 0,
    "productsCount": 0
  },
  {
    "id": 2,
    "name": "Networking",
    "appscount": 1,
    "vxFscount": 15,
    "productsCount": 16
  },
  {
    "id": 3,
    "name": "Automotive",
    "appscount": 2,
    "vxFscount": 3,
    "productsCount": 5
  },
  {
    "id": 4,
    "name": "Media",
    "appscount": 0,
    "vxFscount": 6,
    "productsCount": 6
  }
]
```

next are ways to get authorized requests. You need to have an account in the 5GinFIRE portal


## Authorization via X-APIKEY Header

You can get your APIKEY by the portal:
![Userinfo](/uploads/portal/userinfo.png "Userinfo")

Here is an authorized request with X-APIKEY example: 


```sh
curl -v -H "X-APIKEY:ec6a5be8-66bf-4351-e830-"  https://portal.5ginfire.eu/5ginfireportal/services/api/repo/admin/vxfs
```
X-APIKEY is generated when you create an account.


## Authorization via JSESSIONID cookie 

Here is an authorized request with cookie example: 


```sh
curl -v -H "Content-Type: application/json" -X POST --data '{"username":"admin", "password":"changeme"}' https://portal.5ginfire.eu/5ginfireportal/services/api/repo/sessions
```
example response :

```json
{
	"username": "admin",
	"password": "",
	"portalUser": {
		"id": 1,
		"organization": "5GinFIRE",
		"name": "Portal Administrator",
		"email": "auser@example.com",
		"username": "admin",
		"password": "",
		"active": true,
		"currentSessionID": "5ec34075-1a12-46d8-97ec-b9e1ab064666",
		"roles": [
			"PORTALADMIN"
		]
	}
}
```

In the following requests JSESSIONID cookie value is equal to the currentSessionID (and JSESSIONID given from server). 
Must be present for authenticated requests








[^1]: https://www.openapis.org/.