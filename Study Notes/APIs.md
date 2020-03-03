
- [API](#api)
  - [Latency](#latency)
  - [Partial failure](#partial-failure)
  - [Terms](#terms)
  - [Basic Auth](#basic-auth)
  - [API vs Web Service](#api-vs-web-service)
  - [Questions:](#questions)
  - [API Principles](#api-principles)
  - [Payload](#payload)
  - [HATEOAS (API should provide enough information to the client to interact with the server)](#hateoas-api-should-provide-enough-information-to-the-client-to-interact-with-the-server)
    - [HATEOAS Principle](#hateoas-principle)
  - [Swagger in Spring](#swagger-in-spring)
  - [SOAP (Simple Object Access Protocal)](#soap-simple-object-access-protocal)
  - [Terms](#terms-1)
  - [API Modeling Tips](#api-modeling-tips)
  - [Creating API definition](#creating-api-definition)
  - [Types of relationships](#types-of-relationships)

# API

## Latency

* The time it takes for a request to responde.

## Partial failure

* Then the server or network fail to response.

* Make sure you handle partial failures.

## Terms

* Authentication
* Authorization
* Basic Authentication (Basic Auth)
* API key
* HATEOAS
* Payload


## Basic Auth
* Only requires Username and Password. The server converse it into a single 64 base encode value and compares it with the user data it has stored. If it fails, throw a 401 error code.
* API Key, a unique key to authenticate


## API vs Web Service

* Web Service is a way of communication among different applications or languages, usually over the network, using SOAP or REST.
* API is any mean or interface of communication among programs, apps, etc., over the network or not.

## Questions:

1) What are the two most common concerns when using web services
    * latency and partial failures
2) What feature allows the service provider and the service client to be written in different programming languages
    * language transparency
3) What does the use of web service reduce in order to deliver more powerful applications
    * development time

## API Principles

* Resources (in HTML, XML, plain text, json)
* Stateless (servers doesn't remember previous requests)

## Payload
* Data sent between client and server


## HATEOAS (API should provide enough information to the client to interact with the server)
* Hypermedia
* As
* The
* Engine
* Of
* Application
* State

### HATEOAS Principle
* Resources should be discoverable through the publication of links
* Links specifies what the customer can and cannot do.


## Swagger in Spring

* Add a Swagger dependency in the Spring POM file, this way you have access to a url in your app where Swagger will show the end points it discovered.


## SOAP (Simple Object Access Protocal)

* SOAP supports ACID
* WSDL (Web Service Description Language) specifies what the client can be performed by the web service. It contains information needed, metadata.


* SOAP is mainly used in enterprise-level web services like:
    * Finalcial services
    * Payment gateways
    * etc.


## Terms
* WSDL

## API Modeling Tips

* Keeps notes
* Have consistency
* Documment everything
* Remember document gaps and questions

## Creating API definition

* Resources are nouns (like items, carts, order, etc)
* Add the actions (verbs) related to those nouns
  * List items, view items, view cart, view order, cancel order, etc.
* Then map the HTTP Methods to those nouns, like GET, DELETE, PUT, POST

## Types of relationships

* Independent
  * And endpoint exits by itself
* Dependent
  * An endpoint requires another one to make sense. Like order needs a cart to proceed.
* Associate
  * Can be Independent or Dependent, but needs more information to describe it



