
# Pending

What is Amazon S3
Integration testing tools
GAUNTIT

---

# Continuous Integration

The practice of automatically building and unit testing an entire application frequently, ideally on every source code check-in. Dozens of times a day if needed.

**Keywords**: testing the entire app, frequently, after every check-in, many times.

# Continuous Delivery

The practice of deploying every build to a production-like environment and performing automated integration and _acceptance_ testing.
Check functionality and performance.

**Keywords**: deploying to production-like env, integration and acceptance tests, function, performance.

Benefits:

* Lowered cycle time
* Better security
* More time to be productive
* etc.

# Continuous Deployment

The practice of automatically deploying every build to production after it passes its automated tests.

**Keywords**: deploy to production after tests.

---


## Build Pipeline

Is a sequence of operation.

---

## Tools

* Source Code
* Version Control
* Build System (watches the code for changes and executes whatever pipeline has to do with it to build it)
* Build Tool (compiles, builders, mvn, docker, etc)
* Unit Tests
* Integration Tests
* Artifacts (package the code, like in .jar, .war, etc)
* Artifact Repo (where you put your artifact)
* Deployment Server
* Deployment tool
* Integration Tests
* E2E Tests
* Production Environment

# Notes

* Jenkins is a build system

* Always use version control
* Commit often
* Don't commit broken code

# Terms

* Branch by Abstraction
* Pre commit hooks (To make sure the commit includes something, etc) 
* DEV PM
* Abao


## CIRCLECI
Is a CI builder.

# A CI Culture

* Run tests locatlly before commiting
* Don't commit new code to broken builds
* Don't leave the build broken
* Don't remove tests that fail
* Use notifications to update your build progress
* Ansible (to deploy code)
* Bamboo (a deploy system)
* Cheff (a deploy system)

# Building Artifacts

Build and distribute your code as package artifact. So you make sure what you tested is actually what is going to production.

Build it, test it and package it.

If you build your app with specific library version, compiler version, framework version, etc., then you test is invalidated if you change any of that.

A build with no code changes, should not produce a different result.

Deploy the same artifacts in all environments or similar, the same way.

## Nexus (to manage artifact repositories)

Jenkins > Nexus plugin

# Testing

* Unit Testing
* Integration Testing
* End-to-End (E2E) Testing
* Security Testing (dynamic and static)
* Shift Left (testing)
* Test Fixture (testing)
* System under test (SUT)
* Cycle time (testing)
* Lead time (testing)
* Mock (testing)


## Testing philosophy

* TDD
* BDD (Behaviour-driven development)
* Acceptance test-driven development

---


## Separate Deploy and Release

* Blue/green deployments (have at least 2 production servers, deploy and test in one, once that is ready, swap it and go to the other)

* Feature flags (toggle) (be able to turn on and off functionalities)







