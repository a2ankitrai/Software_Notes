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
