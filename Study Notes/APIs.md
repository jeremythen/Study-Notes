
- [API](#api)
  - [Latency](#latency)
  - [Partial failure](#partial-failure)
  - [Basic Auth](#basic-auth)
  - [API vs Web Service](#api-vs-web-service)
  - [Questions:](#questions)
  - [API Principles](#api-principles)
  - [Payload](#payload)
  - [HATEOAS (API should provide enough information to the client to interact with the server)](#hateoas-api-should-provide-enough-information-to-the-client-to-interact-with-the-server)
    - [HATEOAS Principle](#hateoas-principle)
  - [Swagger in Spring](#swagger-in-spring)
  - [SOAP (Simple Object Access Protocal)](#soap-simple-object-access-protocal)
  - [Terms](#terms)
  - [API Modeling Tips](#api-modeling-tips)
  - [Creating API definition](#creating-api-definition)
  - [Types of relationships](#types-of-relationships)
  - [Terms](#terms-1)
- [Validating Your API](#validating-your-api)
  - [Act as if the API exists](#act-as-if-the-api-exists)
- [SOAP vs REST](#soap-vs-rest)
  - [SOAP](#soap)
  - [REST](#rest)
- [HTTP](#http)
  - [Header](#header)
    - [HTTP Response Codes](#http-response-codes)
      - [2xx (Success)](#2xx-success)
      - [3xx (Redirect)](#3xx-redirect)
      - [4xx (Client Error)](#4xx-client-error)
      - [5xx (Server Errors)](#5xx-server-errors)
  - [Content-Type](#content-type)
    - [Media-Type (how the content is format)](#media-type-how-the-content-is-format)
  - [Payload](#payload-1)
- [The Six constraints](#the-six-constraints)
  - [1 APIs should be designed for **Client-Server Architecture**](#1-apis-should-be-designed-for-client-server-architecture)
  - [2 APIs should be **Stateless Architecture**](#2-apis-should-be-stateless-architecture)
  - [3 Cacheable](#3-cacheable)
  - [4 Layered Systems](#4-layered-systems)
  - [5 Code on Demand](#5-code-on-demand)
  - [6 Uniform Interfaces](#6-uniform-interfaces)
- [API Design Patterns](#api-design-patterns)
  - [Authentification (AuthN)](#authentification-authn)
    - [Is stablishing **who you are**.](#is-stablishing-who-you-are)
  - [Authorization (AuthZ)](#authorization-authz)
    - [Is stablishing what **you are allowed to do**.](#is-stablishing-what-you-are-allowed-to-do)
  - [API Key](#api-key)
    - [Don't create your own AuthN/AuthZ Protocol. Don't create your won hashing algorithm, etc.](#dont-create-your-own-authnauthz-protocol-dont-create-your-won-hashing-algorithm-etc)
  - [OAuth 2.0](#oauth-20)
- [API Versioning](#api-versioning)
  - [Accept Header](#accept-header)
  - [Structuring the Payoad with HyperMedia Types](#structuring-the-payoad-with-hypermedia-types)
- [HyperMedia](#hypermedia)
- [Documentation](#documentation)

# API

## Latency

* The time it takes for a request to responde.

## Partial failure

* Then the server or network fail to response.

* Make sure you handle partial failures.

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
* Collection+JSON
* HAL
* Media Type
* HyperMedia Types
* Twilio
* Okta
* Content Negotiation
* ETag
* Jekyll and Slate
* SDK
* Microframwork

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

## Terms

* Authentication
* Authorization
* Basic Authentication (Basic Auth)
* API key
* HATEOAS
* Payload
* Microframework (hapi.js, slim, silex)

# Validating Your API

## Act as if the API exists

* List the end points
* List the parameters
* List the response codes
* Create the documentation
* Documentation doesn't need to be perfect
* Make sure to let users know the work is not done
* Have a draft of your api and doc

# SOAP vs REST

## SOAP
* Fixed process
* Losts of docs up front
* Detailed scenarios
* Complex error handling

## REST

* Few requirements
* Docs discovered as you go
* Flexible, based on needs
* Flexible, based on patterns

# HTTP

## Header

### HTTP Response Codes

#### 2xx (Success)

* 200 (Ok)
* 201 (Created)
* 202 (Accepted)
* 204 (No Content)

#### 3xx (Redirect)

* 301 (Moved Permanently)
* 302 (Moved Temporarily)

#### 4xx (Client Error)

* 400 (Bad Requset)
* 401 (Authentication)
* 403 (Forbidden, no permission)
* 404 (Not Found)

#### 5xx (Server Errors)

## Content-Type

Is the type of Payload.

For normal web browsers, it could be text/html
For APIs, would be application/json

### Media-Type (how the content is format)


## Payload

# The Six constraints

## 1 APIs should be designed for **Client-Server Architecture**

* Server serving the client

## 2 APIs should be **Stateless Architecture**

* Client should send all state needed to the server every time. Server should not hold the state of the client.

## 3 Cacheable

* Avoid unnecessar work, by caching. Idempotent.
* GET, PUT and DELETE should be idempotent, or safe.

## 4 Layered Systems

* Clients may not be talking to the server or IP address directly. Layers of abstraction can be placed in between. Like DNS, laod balances, caching servers, logging, API Gateways, apigee, etc.

## 5 Code on Demand

* Like how the browser retrieves and executes Javascript code that is comming from the server. The client doesn't need to know what is in the code, but how to execute it.

## 6 Uniform Interfaces

* Identification of resources
* Manipulation of resources through these representations
* Self-descriptive messages
* HATEOAS

# API Design Patterns

## Authentification (AuthN)

### Is stablishing **who you are**.

## Authorization (AuthZ)

### Is stablishing what **you are allowed to do**.

## API Key

An API key ban be used to authenticate and authorize.

### Don't create your own AuthN/AuthZ Protocol. Don't create your won hashing algorithm, etc.

## OAuth 2.0

Use OAuth for authorization

# API Versioning

## Accept Header

Defining how we want the data.

This is to inform the server that this is the data type in the format that it understands.
The data can be XML or JSON.

A media type is a structure that both the client and the servicer know how to handle.

Can establish th eversion of the media type (and resource)

Is a good idea **to put the version on the url itself**, so is easy to see and can be copied and pasted with it.

## Structuring the Payoad with HyperMedia Types

* Avoid creating your own JSON formats, media types, etc.

There are Payload structures already created, like:

* Collection+JSON
* HAL
* Ion

# HyperMedia

# Documentation

* We need code snippet friendly, with syntax highliting.
* Easy to update
* Searchable (with SEO)