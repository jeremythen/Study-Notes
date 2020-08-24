





```yaml

# Quering data
query {
  products(first: 10) {
    edges {
      cursor
      node {
        id
        name
      }
    }
  }
}


# Using cursors to query data after it:
query {
  products(first: 10, after: "WyJjb2RlLWRpdmlzaW9uLXQtc2hpcnQiXQ==") {
    edges {
      cursor
      node {
        id
        name
      }
    }
  }
}


# Before
query {
  products(first: 10, before: "YXJyYXljb25uZWN0aW9uOjQ==") {
    edges {
      node {
        id
        name
      }
    }
  }
}


# Page info

query {
  products(first: 10) {
    edges {
      cursor
      node {
        id
        name
      }
    }
    pageInfo {
      hasNextPage
      hasPreviousPage
      startCursor
      endCursor
    }
  }
}

```


# Errors

## Query-level errors
Any error on the query like an unknown property

```yaml

# Query

{
  me {
    fullName # Where this property doesn't exist
  }
}

# Response

{
  "error": {
    "errors": [
      {
        "message": "Cannot query field \"fullName\" on type \"User\". Did you mean \"firstName\" or \"lastName\"?",
        "locations": [
          {
            "line": 3,
            "column": 5
          }
        ]
      }
    ]
  }
}


```

## Data-level errors
When a user send invalid data like the wrong email

```yaml

# Query

mutation {
  accountRegister(
    input: {
      email: "customer@example.com"
      password: ""
      redirectUrl: "http://demo.saleor.io/reset-password/"
    }
  ) {
    user {
      email
    }
    accountErrors {
      field
      code
    }
  }
}

# Response

{
  "data": {
    "accountRegister": {
      "user": null,
      "accountErrors": [
        {
          "field": "email",
          "code": "UNIQUE"
        }
      ]
    }
  }
}

```

## Permission errors

```yaml

# Query

{
  staffUsers(first: 20) {
    edges {
      node {
        id
      }
    }
  }
}

# Response

{
  "errors": [
    {
      "message": "You do not have permission to perform this action",
      "locations": [
        {
          "line": 2,
          "column": 3
        }
      ],
      "path": ["staffUsers"]
    }
  ],
  "data": {
    "staffUsers": null
  }
}


```

# Products

```yaml
# Searching with filter
{
  products(first: 2, filter: {search:"juice"}) {
    edges {
      node {
        id
        name
        seoTitle
        seoDescription
        description
        descriptionJson
        isPublished
        productType {
          id
        }
      }
    }
  }
}

# Sorting products

{
  products(
    first: 2
    sortBy: { field: MINIMAL_PRICE, direction: ASC }
  ) {
    edges {
      node {
        name
        minimalVariantPrice {
          amount
          currency
        }
      }
    }
  }

# With variants
# Query
{
  products(first: 1) {
    edges {
      node {
        id
        name
        variants {
          id
          name
        }
      }
    }
  }
}

# Response
{
  "data": {
    "products": {
      "edges": [
        {
          "node": {
            "id": "UHJvZHVjdDo3Mg==",
            "name": "Apple Juice",
            "variants": [
              {
                "id": "UHJvZHVjdFZhcmlhbnQ6MjAz",
                "name": "1l"
              },
              {
                "id": "UHJvZHVjdFZhcmlhbnQ6MjA0",
                "name": "2l"
              },
              {
                "id": "UHJvZHVjdFZhcmlhbnQ6MjAy",
                "name": "500ml"
              }
            ]
          }
        }
      ]
    }
  }
}



# Product with pricing info

{
  products(first: 1) {
    edges {
      node {
        id
        name
        pricing {
          onSale
          discount {
            currency
            gross {
              currency
              amount
            }
            net {
              currency
              amount
            }
            tax {
              amount
              currency
            }
          }
          priceRange {
            start {
              currency
              
            }
            stop {
              currency
            }
          }
        }
        variants {
          id
          name
        }
      }
    }
  	
  }
}


# With images

{
  products(first: 1) {
    edges {
      node {
        id
        name
        thumbnail(size: 100) {
          url
          alt
        }
        images {
          url(size: 100)
          alt
        }
      }
    }
  }
}

```