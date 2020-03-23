
 # Terms

 * Doubles
   * Dummies
   * Fakes
   * Spies
   * Stubs
   * Mocks
 * Confidence Levels
   * Write tests to feel confident that changes to the code will be backed by the tests.
 * Code Coverage tools
   * Let you identify what parts of your codebase are run during tests.
 * Code Coverage metrics
   * Can be used to decide what parts of your codebase need tests.


# Patterns

Arrange-Act-Assert


# Notes

## General

You can use a phpunit.xml file to put the test information, test suit, etc.

## Running tests

You can run all the tests in a directory named 'tests':

> phpunit tests

Or a specific class:

> phpunit tests/ReceiptTest.php

With a filter on a specific mathod named 'testTax':

> phpunit tests --filter=testTax

With a filter on a specific mathod named 'testTax' on a class named ReceiptTest:

> phpunit tests --filter=ReceiptTest::testTax

To run a specific test suit named 'app':

> phpunit --testsuit=app

To run a specific method named 'textTax' on a specific test suit named 'app':

> phpunit --testsuit=app --filter=testTax


# Doubles

## Doubles uses

* Replace a dependency
* Ensure a condition occurs
* Improve the performance of out tests

