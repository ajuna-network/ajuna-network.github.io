---
layout: default
title: Testing
permalink: /guides/testing
---

[rust-unit-testing]: https://doc.rust-lang.org/rust-by-example/testing/unit_testing.html
[substrate-testing]: https://docs.substrate.io/v3/runtime/testing/
[polkadot-js]: https://docs.substrate.io/v3/integration/polkadot-js/
[substrate-client-libraries]: https://docs.substrate.io/v3/integration/client-libraries/

# Testing

This guide expresses some general ideas about how we think about testing, both development, and product driven.

We have a few objectives for testing:
- automate as much as possible
- easy to write
- easy to understand
- pure, tests should not rely on other tests
- pragmatic, we do not need to test simple things

## Types

We have a few main types as we walk ourselves up the testing triangle. Starting from the bottom, we have:

- Unit
- Integration
- End to End
- Acceptance testing

So what do the types mean to us?

### Unit

Unit testing is our most granular level of testing. The purpose of a unit test is to prove under certain conditions that our function will work as expected. 
There is an argument to be made that it is the inverse, but for brevity, we will assume the positive notation.

In terms of tools, we have native capabilities in our ecosystem. We can write unit tests in a variety of languages.

[Unit testing in Rust][rust-unit-testing]

### Integration

Integration tests rely on some other effect. Integration tests may involve a database operation, network call, or another external effect. 

Sometimes referred to as white box testing, the idea is that it will open up the box and test outputs expected from each service.

An example might be:
- if I queue a game:
    - was it added to the registry?
    - did it have the right players?
    - did it have the correct block information?
    - can I see it in the registry?

Of course, a developer might mock this data depending on the approach, But ultimately the moving parts concerning the test should be moving; this will lead to a much more testable test.

#### Integration: Substrate

Substrate has its own [Mock Runtime][substrate-testing]. This runtime will help us with block production, genesis config.


For development testing, a tool to help verify features:
[Polkadot-JS][polkadot-js]

We can also have a look here if we want to build our integration test suites in the future:
[Client Libraries][substrate-client-libraries]

### End to End(E2E)

E2E testing covers a business process; it could be something as significant as user login, creating a new game, or gameplay.

Sometimes referred to as Black Box Testing, the test does not necessarily care about what happens at a granular level, just that what comes out is correct.

It usually involves every end of the system, from the front to the back.

WIP: 
- Add some tools here, tying in front end work

### Acceptance

Acceptance testing can be done automatically by the process of Continuous Integration. 
The product team may manually accept it. 

Acceptance tests could be:
- QA
- Product Manager
- Product Owner
- Stakeholders

Acceptance tests might also involve some exploratory manual testing.