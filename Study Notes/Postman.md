

# Global and Environment

## Variables

### Initial Value

Is shared with your collection.

### Current Value

Is private to you and is not shared when you share your collection. It's saved locally.


# Notes

You can create Global Variables or create them in specific Environment

You can run an entire Collection


## Setting Next Request to execute

In the Tests tab put:

```javascript
postman.setNextRequest('Postman Echo PUT'); // Where 'Postman Echo PUT' is the name of the request.
```

Save it and open the collection browser to run it.

## Using data from a response of a request in another request

Go to Tests tab
Put code like this:

```javascript
// Parsing the response returned by the request.
var jsonData = pm.response.json();

// Extracting the token from the response and setting it as a global variable.
pm.globals.set("newToken", jsonData.headers['postman-token']);
```

