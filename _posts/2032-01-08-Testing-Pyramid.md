---
layout: post
title: Some ideas on software testing
date: 2023-01-08 08:00:00 +0000
categories: [Software Testing, Quality]
tags: [Test Pyramid]
image:
  path: /images/kirkjufell.jpg
  alt: A photo I took of Kirkjufell in Iceland from November 2022; it's not a pyramid but I like the photo
---

## What is quality?

The degree to which a component or system satisfies the stated and implied needs of its various stakeholders. ― ISTQB

“Quality is not an act, it is a habit”. ― Aristotle

“Software never was perfect and won’t get perfect. But is that a license to create garbage? The missing ingredient is our reluctance to quantify quality.” ― Boris Beizer

“Quality means doing it right even when no one is looking” ― Henry Ford

## What is testing?

James Bach and Michael Bolton make a distinction between testing and checking.

Testing is the process of evaluating a product by learning about it through experimentation, which includes to some degree: questioning, study, modelling, observation and inference.

 *A test is an instance of testing.*

Checking is the process of making evaluations by applying algorithmic decision rules to specific observations of a product.

 *A check is an instance of checking.*

So, not all testing can be automated!

## What is an integration or unit test?

I think that the most confusing thing about testing is the word testing (Feathers, 2016)

**We have a problem!**

The software development community hasn’t agreed and settled on well defined terms around testing.

**Solution**

We shouldn’t get too hung up on ambiguous terms, it doesn’t matter if an integration test here doesn’t match a definition at another organisation.

What’s important is that we’re clear about the different types of test that we want to write.

## Different types of tests

- Unit tests
- Integration tests
- Component tests
- Integration contract tests
- End-to-end tests
- Exploratory tests
- Security / Pen tests
- Performance tests
- Other non-functional tests, such as testing accessibility, usability, failover and recovery and compatibility.

## Unit tests

A unit test exercises the smallest piece of testable software in the application to determine whether it behaves as expected. (Martin Fowler)

- Typically exercises functions, methods and classes.
- They should be short and sweet, ideally the smaller the unit the better as this provides more granular detail on how the code behaves.
- Unit tests should not have any external dependencies, mocks and monkey-patching are for this.
- The idea is to have many smaller tests that execute within a matter of seconds rather than minutes.
- Unit testing enables practices such as Test-driven Development (TDD), where tests are written before the feature code, the feature code is then written to make the tests pass.

## Integration tests

Verifies the communication paths and interactions between components to detect interface defects.

- Some define integration testing as testing the entire stack of the application, connected to other applications.
- Others define it as narrowly testing one integration point at a time by replacing separate service and databases with test doubles.
- Service calls to REST APIs can be considered integration tests.
- Integration tests should be black-box and only interact with live instances of the product, rather than the code.

## End-to-end tests

Verifies that a system meets external requirements and achieves its goals, testing the entire system, from end to end.

- End-to-end tests cover a user journey or path through a system
- Typically they interact with the system as a user would
- Manipulating a system through a UI can be considered a E2E testing as it requires the full stack to be present.
- End-to-end tests usually run against a system deployed in a environment as close to production as possible.

## The Testing Pyramid

In 2009, Mike Cohn published “Succeeding with Agile” and introduced the model of a test automation pyramid.

It has since been widely adopted since the mid 2000’s as the industry-standard guideline for functional test case development.

Mike Wacker from the Google Testing Blog states how Google often suggests a 70/20/10 split: 70% unit tests, 20% integration tests, and 10% end-to-end tests (Wacker, 2015); which demonstrates how most of the testing should happen lower down in unit and integration tests.

![Software Testing Pyramid]({{ site.baseurl }}/images/testing_pyramid.png)

**Alternative view?**

We can also view the test pyramid upside down as a bug filter.

Fowler (2012) states if you get a failure in a high level test; then you have a bug in your functional code and also a missing or incorrect unit test.

![Drawing of the Test Pyramid upside down re-imagined as a bug filter]({{ site.baseurl }}/images/bug_filter.jpg)

## We don’t want an ice cream cone!

Alister Scott’s ice-cream cone antipattern occurs, when most of the system is tested by higher layer tests, such as relying on UI tests or manual testing.

![Software Testing Ice-cream Cone Anti-Pattern from watirmelon.com]({{ site.baseurl }}/images/icecream-cone.jpg)

**Disadvantages**

- Costly to run and develop and maintain
- Timely feedback loop as tests take longer to run
- Makes it difficult to make changes and refactor confidently due to few or no unit tests
- Bugs takes longer to diagnose
- Tests are broken by new changes regularly and there can be a reliance on "testing" to fix them

## Key points

- Tests should catch bugs as close to the root cause as possible and unit tests are the first line of defense.

- Unit tests are cheaper to write and maintain and quicker to run, let’s write more of them.

- Tests on the upper levels are more expensive to write and maintain and are slower to run, so we want lots of unit tests, some integration tests and a few end-to-end tests.

- A risk-based strategy to push testing down the test pyramid is better than having many higher-level tests.

- The test pyramid is a guideline and not a rule, the shape of pyramid is less important than the placement of the layers - the sense of “do more at lower levels” is the general thought.

- Testing and quality is a team effort!

## References

Cohn, M., 2009. Succeeding With Agile. Pearson.

Feathers, M., 2016. Michael Feathers - Characterization Testing. [online] Michaelfeathers.silvrback.com. Available at: <https://michaelfeathers.silvrback.com/characterization-testing>

Fowler, M., 2012. Test pyramid. [online] martinfowler.com. Available at: <https://martinfowler.com/bliki/TestPyramid.html>

Fowler, M., 2014. Testing Strategies In A Microservice Architecture. [online] martinfowler.com. Available at: <https://martinfowler.com/articles/microservice-testing>

Gregory, J. and Crispin, L., 2015. More Agile Testing. Upper Saddle River, N.J: Addison-Wesley.

Vocke, H., 2018. The Practical Test Pyramid. [online] martinfowler.com. Available at: <https://martinfowler.com/articles/practical-test-pyramid.html>

Wacker, M., 2015. Just Say No To More End-To-End Tests. [online] Google Testing Blog. Available at: <https://testing.googleblog.com/2015/04/just-say-no-to-more-end-to-end-tests.html>
