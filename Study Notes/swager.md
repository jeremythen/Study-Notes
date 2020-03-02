
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



# Examples

## Customer 

```yaml

openapi: 3.0.0
# Added by API Auto Mocking Plugin
servers:
  - description: SwaggerHub API Auto Mocking
    url: https://virtserver.swaggerhub.com/jeremythen/customer/1.0.0
info:
  description: This is an API for HPlusSport customers
  version: "2.0.0"
  title: Customers API
  contact:
    email: you@hplussport.com
  license:
    name: Apache 2.0
    url: 'http://www.apache.org/licenses/LICENSE-2.0.html'
tags:
  - name: customer
    description: customer relacted calls
  - name: developers
    description: Operations available to regular developers
paths:
  /customer:
    get:
      tags:
        - customer
      summary: searches customer
      operationId: searchCustomer
      description: |
        By passing in the appropriate options, you can search for
        available customer in the system

      responses:
        '200':
          description: search results matching criteria
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Customer'
        '400':
          description: bad input parameter
components:
  schemas:
    Customer:
      type: object
      required:
        - firstName
        - lastName
      properties:
        customerNumber:
          type: string
          format: uuid
          example: d290f1ee
        firstName:
          type: string
          example: John
        lastName:
          type: string
          example: Smith
        phoneNumber:
          type: string
          example:  555-555-555

```

## Catalog

```yaml

openapi: 3.0.0
info:
  title: Catalog API
  version: 1.0.0
servers:
  - description: SwaggerHub API Auto Mocking
    url: https://virtserver.swaggerhub.com/jeremythen/catalog/1.0.0
tags:
  - name: product
    description: This is a product related operation
paths:
  /product/{productId}:
    get:
      tags:
        - product
      parameters:
        - in: path
          name: productId
          required: true
          schema:
            type: integer
            example: 12345
        - in: header
          name: customer-security-header
          required: false
          schema:
            type: integer
            example: 12312-323422-2323
      responses:
        200:
          description: This is a list of the products in the catalog
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Product'
        500:
          $ref: '#/components/responses/500ApiError'
  /product:
    post:
      security:
        - password: [write]
      tags:
        - product
      description: Add a product to the catalog
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Product'
      responses:
        200:
          description: The product has been created
          content:
            aplication/json:
              schema:
                $ref: '#/components/schemas/Product'
            application/xml: # This is to make available others Media Type
              schema:
                $ref: '#/components/schemas/Product'
        500:
          $ref: '#/components/responses/500ApiError'
    get:
      tags:
        - product
      parameters:
        - $ref: '#/components/parameters/PageNumber'
        - $ref: '#/components/parameters/PageSize'
      responses:
        200:
          description: This is a list of the products in the catalog
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Product'
        500:
          $ref: '#/components/responses/500ApiError'
components:
  securitySchemes:
      password:
        type: oauth2
        flows:
          password:
            tokenUrl: 'http://example.com/oauth/token'
            scopes:
              write: allows modifying resources
              read: allows reading resources
  parameters: # parameters object
    PageNumber: # Custom parameter name
      in: query
      name: pageNumber
      description: Page number to return
      required: false
      schema:
        type: integer
        example: 1
    PageSize:
      in: query
      name: pageSize
      description: Number of results in the page
      required: false
      schema:
        type: integer
        example: 10
        maximum: 100
  schemas: # Schema object
    Product:
      type: object
      required:
        - name
      properties:
        id:
          type: integer
          example: 400
        name:
          type: string
          example: Lemon Water
        description:
          type: string
          example: Lemon Water
        image_title:
          type: string
          example: mineral-water-lemon-lime
        image:
          type: string
          example: https:/hplussport.com/images/123
  responses: # responses object
    500ApiError: # Custom name
      description: This is an unexpected error
      content:
        application/json:
          schema:
            type: object
            properties:
              statusCode:
                type: string
                example: 500
              message:
                type: string
                example: This is an error

```