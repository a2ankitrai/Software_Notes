# REST_notes


https://stackoverflow.com/questions/2840275/whats-the-best-source-for-learning-how-to-create-restful-apis-in-java

REST APIs shoule be about resources not functionalities. Functionality MUST not be duplicated across the API, but rather that resources are expected to be re-used as needed across use cases.

## HTTP Methods

| HTTP        	  | Description   |  
| :-------------: |:-------------|  
| `GET`           | To *retrieve* a resource. |  
| `POST`          | To *create* a resource, or to *execute* a complex operation on a resource.      |  
| `PUT`           | To *update* a resource.    |   
| `DELETE`        | To *delete* a resource.    |  
| `PATCH`         | To perform a *partial update* to a resource.      |  


- The actual operation invoked MUST match the HTTP method semantics as defined in the table above.

- The `GET` method MUST NOT have side effects. It MUST NOT change the state of an underlying resource(s).

- `POST`: method SHOULD be used to create a new resource in a collection.

- The `POST` method SHOULD be used to create a new sub-resource and establish a relationship to it from the main resource.

- The `PUT` method SHOULD be used to update resource attributes or to establish a relationship from a resource to an existing sub-resource; it updates the main resource with a reference to the sub-resource.

## HTTP Headers

The purpose of HTTP headers is to provide metadata information about the body or the sender of the message in a uniform, standardized, and isolated way. HTTP header names are NOT case sensitive.

- HTTP headers SHOULD only be used for the purpose of handling cross-cutting concerns.

- API implementations SHOULD NOT introduce or depend on headers.

- Headers MUST NOT include API or domain specific values.

- If available, HTTP standard headers MUST be used instead of creating a custom header.


---

## Difference between PUT and PATCH

**PUT** - replace the ENTIRE RESOURCE with the new representation provided

**PATCH** - replace parts of the source resource with the values provided AND|OR other parts of the resource are updated that you havent provided (timestamps) AND|OR updating the resource effects other resources (relationships)

The difference between the PUT and PATCH requests is reflected in the way the server processes the enclosed entity to modify the resource identified by the Request-URI. In a PUT request, the enclosed entity is considered to be a modified version of the resource stored on the origin server, and the client is requesting that the stored version be replaced. With PATCH, however, the enclosed entity contains a set of instructions describing how a resource currently residing on the origin server should be modified to produce a new version.
 
The HTTP PATCH method should be used whenever you would like to change or update just a small part of the state of the resource. You should use the PUT method only when you would like to replace the resource in its entirety. Note that PATCH is not a replacement for PUT or POST, but just a way of applying a delta update to a resource representation. Roy Fielding, who authored the REST architectural style and many web standards, said that he created PATCH because “partial PUT is never RESTful.”





























---
