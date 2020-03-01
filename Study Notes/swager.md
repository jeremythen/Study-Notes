
# Terms

* Design-first approach
* OAS (Open API Specification), defined a standar, programming-language-agnostic interface description for REST APIs.
* Smartbear
* hplussport.com (fictional sport store to test APIs)

## APIGEE
* Is an API management tools. It manages security, requests, etc.

# Swagger
* Create, design, document and generate code for API.

* Swagger Editor
* Swagger UI
* Swagger Codegen (Build client SDKs from API definitions)



http-server swagger-editor -a 127.0.0.1 -p 8081

http-server swagger-ui -a 127.0.0.1 -p 8082 // Go to /dist
http-server swagger-ui -a 127.0.0.1 -p 8083

## OAI:
* Int GitHub, OpenAPI-Specification

# OpenAPI 3.0 objects

* info (info about this API. Required)
* servers
* security
* paths (the paths definitions like get, post, etc. Required)
* tags (metadata)
* externaldocs (links to external apis)
* components (you can reuse components)


---

## To create a reusable component:

```yaml
components:
  schemas:
    Product:
        // Put whatever part you want to reuse.

```

To use it, in any other schema area, add:

```yaml

    $ref: '#/components/schemas/Product'

```

# SwaggerHub

## Public API

* Click the API version an the on the Publish API button.
* One the API is published, you cannot edit it.
* To 'edit' the API, click on the API version and 'Add New Version'
* To see the differences of the two API versions, click on the API version and on 'Compare Versions"

# Tags

## Tags are helpful to group endpoints

* At the level of info and paths objects, put:

```yaml

tags:
    - name: product

```

* And, at any get, post, etc., requests, put:

```yaml

tags:
    - product

```

## Delete API

* Click on it's name, thne on Delete API

## Security

* use security object.

```yaml
    security:
        - password: [write]
```
* Having in components

```yaml

securitySchemes:
      password:
        type: oauth2
        flows:
          password:
            tokenUrl: 'http://example.com/oauth/token'
            scopes:
              write: allows modifying resources
              read: allows reading resources

```

# Domains

* Domains are useful for reusing schemas, etc.
* Create domain by click the + button and Create Domain.
* Specify schemas on that domain, and then $ref it with the URL of where that swagger domain is.


## Standardization

* Click on a domain Settings icon, Standardization and select or add custom standards.
* This helps to enforce quality, standards, making sure things that are expected are there, etc.

# Auto Mock

## To create a mocking service to test your API through SwaggerHub, so it uses the example data as mock

* Click on the name of the API
* Integrations
* Add New Integration
* API Auto Mocking
* Add it to your API with:

```yaml
servers:
  - description: SwaggerHub API Auto Mocking
    url: https://virtserver.swaggerhub.com/jeremythen/catalog/1.0.0
```

# Collaboration

* Domain Settings
* Members
* Invite Members

## Collaboraors on specific APIs

* Get into the API
* Click on Share And Collaborate