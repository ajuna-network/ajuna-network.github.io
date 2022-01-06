---
layout: default
title: Performance Testing
permalink: /guides/testing/performance
---

# Performance testing

This guide expresses some general ideas about how we think about the term performance testing.
It's essential to express the terminology as load testing is simply an umbrella term used to describe any testing involving some deliberate requests.

## Types

We have a few main types as we walk ourselves up the triangle. Starting from the bottom, we have:

within the *codebase*
- Microbenchmarks
- Pallet benchmarks

within the *network*
- Load testing
- Scalability testing
- Soak testing
- Stress testing

So what do the types mean to us?

## Within the codebase

Within the codebase means that we do not need any external tools; we have mechanisms in our arsenal that will allow us to test natively.

### Microbenchmarks

Microbenchmarks are our most granular level of benchmarking.

This benchmarking is for complex, small units of the code base, such as:
- hand-written algorithms
- comparing algorithms

Tools such as [bench](https://crates.io/crates/bench) and [criterion](https://crates.io/crates/criterion) are used to run unit benchmarks. With the latter being more sophisticated.

### Pallet Benchmarks

Pallet benchmarking relates to [substrate benchmarking](https://docs.substrate.io/v3/runtime/benchmarking/) and answers our most important questions around [transaction weight](https://docs.substrate.io/v3/concepts/weight/). 

Pallet benchmarks are an integration-like benchmark test in that it tests a black box of the system due primarily to the fact that calls are generally database reads, network calls, and such.

Tools used are usually the frame benchmarking suite [frame benchmarks](https://docs.substrate.io/rustdocs/latest/frame_benchmarking/macro.benchmarks.html)

## Within the network

Within the network is anything external to the codebase, and we would need an external tool to test it.

What do we want from tools:
- reproducible
- true
- as code

[Drill](https://github.com/fcsonline/drill) is an excellent piece of kit that will allow us to test the network without having hugely differing results since we are not using a garbage collected tool like Gatling or k6 and the like. Garbage collection is vital as we want the system to send the right amount of requests correctly.

### Load testing

Load testing is the most basic form of performance testing; it also has a fair amount of metrics that it can be applied to, for example:
- latency(`L99`, `L95`, etc) under `50` concurrent requests
- throughput under `10` users
- how many errors do we get?
- does it die?

Generally, load testing is done at a whim to answer a bespoke question, and it does not answer all the things we would typically want to know about a system.
It might be a simple API endpoint or a small subset of the system, such as a resource.

### Scalability testing

The maximum number of requests/users that a system can handle under some set parameters.
This testing tends to feed directly into scaling parameters, instancing schemas and sizes of resources.

Some example questions might be: 

- with `4` services running, how many users can we support?
- with `10k` users, to what do we need to scale?
- when does our load balancing strategy fail?
- when should we scale up?
- when should we scale out?

As you can see, some metrics for scalability testing are not directly related to load testing. It usually is:
- users
- error rate
- basic questions
- service CPU
- service memory
- network bandwidth

### Soak testing

Soak testing is quite like scalability testing, although performed under time. 
Generally, the main question is: does it fail? 
Therefore the key to getting a good test is drilling into the definition of failure; things like acceptable error rate at certain times might be applicable.

Some example questions might be:
- If we have `300` users with a derivative of `5%` and the test is run for a week. Do we have an error rate of more than `0.5%?` 
- If we have `30` users and on a particular day we have a peak of `5000` users, can we serve `95%` of the users?

As you can see, the questions tend to be quite specific and around time; note that the time is a parameter.

Also, note that we are not simply sending a straight amount of users; we are sending a derivative of users. 
It's perfectly reasonable to send `30 users` for `30 days`, however.

It generally helps feed into scaling policies and answer some real-world questions.

### Stress testing

Stress testing is a form of load testing that tries to break your system. The most common practice is adding additional users until it dies. Usually, this will stretch the scaling policy of the system and lead to failure.

Cost is an important consideration, so stress tests are relatively short and not in production. Although not impossible.

It does answer a fundamental question, what can we do under what maximum parameters, and how long does it take to fail?

Stress testing is usually what stakeholders or budget coordinators are the most interested in.

### Footnote on performance testing types

They are all quite similar, and there are no held fast rules. But it is essential to use the correct jargon for what you mean.

## Metrics

Standard metrics we want out of performance testing are generally unanimous amongst the industry.

### Users

Users, or requests, refer to the number of concurrent requests made to the system. It could be:

- sending API calls
- sending multiple API calls, such as authenticating, creating a resource, etc
- following a flow of requests
- querying caches


### Latency

Latency is how long it takes to get a response from the system. We generally use the [L99](https://en.wikipedia.org/wiki/99_percentile) and [L95](https://en.wikipedia.org/wiki/95_percentile) as common metrics.

### System

System metrics are usually `CPU%`, `RAM`, `IO`, and `network bandwidth`.

### Error Rate

The error rate is the percentage of requests that fail, or sometimes the raw number of requests that fail.
It could also be the number of times a system is killed or restarted, how many times database operations fail, etc.

Generally, anything exceptional to the system is an error rate.

### Basic questions

The most basic question is "does it die?" commonly refers to an intrinsic error rate.