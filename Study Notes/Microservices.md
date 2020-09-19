Microservice is SOA (Service Oriented Architecture) with emphasis on small ephemeral components

# Building block of DDD

- Ubiquitous Language
- Multilayer Architecture
  - Presentation
  - Application
  - Domain
- Artifacts or DDD
  - Entities
  - Value Objects
    - Only contains attributes, no identity. Opposite of Entities
    - Immutability
  - Services.
    - Part of the domain layer
    - No internal state (stateless)
    - Provides behavior to domain that does not belong to specific single entity or value object
  - Aggregates
    - Defines ownerships and boundaries
    - It is a root entity object that binds collections of objects together and these objects cannot be access or changed directly, only through the root. Like Customer that has the aggregate objects ContactInfo and Address. Doesn't make sense to add an Address if it's not for a user, through that user, for that user.
  - Repository
    - Interacts with storage
  - Factory
    - Required when simple constructor is not enough to create the object (Complex object or Aggregate)
  - Modules
    - Separates the related business objects
    - Helpful in large projects
    - Ubiquitous language can be used here

# DDD: Strategic Design and Principle - Bounded Context

- Bounded Context
  - Should be assignable to a single team
  - Module is a part of the Bounded Context
- Continuous Integration
  - Should have automated tests
- Context Map
  - Shared Kernel
    - Parts of multiple Bounded Context being shared
    - Customer-supplier
      - Relationship between 2 bounded context
      - One bounded context produces, another consumes
    - Conformist
      - A form of customer-supplier
      - Upstream/Downstream relationship
    - Anticorruption layer
      - Part of the domain that interacts with external systems
      - Protects the integrity and originality of the domain model
      - Can clean and format external data
      - Can use Facade, adapters and translators

# Microservices

- Service Registration and Discovery
  - Restaurant Service
  - User Service
  - Booking Service
  - Eureka service discovery
- API Versioning
  - Always use API versioning. The API may change in the future and is betting to manage it with versions.
  - Types:
    - Version in endpoint path (/v1/restaurants)
    - Version as HTTP header
