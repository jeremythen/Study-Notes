# Cypress

## Aliases:

```javascript
cy.get("really_long_selector").as("shortSelector");

cy.get("@shortSelector");

cy.get("@shortSelector").then(($shortSelectorElem) => {
  expect($shortSelectorElem.text()).to.equal("15");
});
```

## Before each:

```javascript
describe("etc", () => {
  beforeEach(() => {
    cy.visit("url");
    //...
  });
});
```

## Snippets

```javascript
// Double click

cy.get("elem").dblclick();

// Getting the value of the in put text and checking if it's 'etc'

cy.get("input").invoke("text").should("equal", "etc");

// Checking checkboxes

cy.get("#checkbox").check();

// Selecting select option

cy.get("theSelect").select("the option");

// Executing specific commands with trigger:

cy.get("selector").trigger("mouseover");
cy.get("selector").trigger("mouseover", 10, 20); // 10 and 20 are x and y coordinates.

// Common assertions

cy.get("selector").should("have.class", "the-class");
cy.get("selector").should("have.css", "background-color", "blue");
cy.get("selector").should("contain", "etc");
cy.get("selector").should("not.contain", "etc");
cy.get("selector").should("have.length", 3);
cy.get("selector").should("exist");
cy.get("selector").should("not.exists");
cy.get("selector").should("be.visible");
cy.get("selector").should("not.be.visible");

// find, to look inside of an element already gotten

cy.get("@list").find(".lsit-item").should("exist");

// Using debugging keyword

cy.get("etc").then(() => {
  debugger;
});
// or
cy.get("etc").trigger("mouseover").debug();
// When is on debug, cypress will print some information in the console and a subject object which is the current object selected.


// Wrap command. When you use then(), to convert that element back to cypress object to use should():

cy.get('h1').then($element => {
    //...
    cy.wrap($element).should(...);
});

// .and command:

// before:

cy.get('h1')
    .should(...)
    .should(...);

// with and:

cy.get('h1')
    .should(...)
    .and(...);


// filter and not commands, like in jQuery:

cy.get('selector')
    .not('p');

cy.get('selector')
    .filter('p');

// Special Characters

cy.get('input')
    .type('This is a test {enter}'); // Putting {enter} in {} will run that key or special character

```

## Environment variables

To set cypress env variables, prefix it with CYPRESS:

> CYPRESS_MY_ENV_VARIABLE="etc"

Then use it in the code like:

```javascript
const myVar = Cypress.env("CYPRESS_MY_ENV_VARIABLE");
```

There are various ways to set env variables:

1. In the system
2. As parameters:
   > npx cypress open --env MY_ENV_VARIABLE='hello'
3. Adding them to the cypress.json file:

```json
{
  "baseUrl": "url",
  "env": {
    "MY_ENV_VARIABLE": "hello"
  }
}
```

4. Creating another file in the root named cypress.env.json:

```json
{
  "MY_ENV_VARIABLE": "hello"
}
```

This way Cypress will load it automatically when it starts running.

## Test doubles

### Sinon Library

```javascript
cy.stub();
cy.spy();

//

cy.stub(apiService, "getUser").returns({ name: "Bill" });

cy.stub(apiService, "getUser").resolves({ name: "Bill" }); // Async promise

cy.stub(apiService, "getUser").rejects({ name: "Bill" }); // Async promise

// spy doesn't mock the calls, it just watches them:

const mySpy = cy.spy(apiService, "getUser");

expect(mySpy).to.be.called;
```

## Activating auto completion

Put this in the first line of the file

```javascript
/// <reference types="Cypress" />
```

Or add file jsconfig.json:

```json
{
  "include": ["./node_modules/cypress", "cypress/**/*.js"]
}
```
