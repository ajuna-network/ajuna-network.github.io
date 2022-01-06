---
layout: default
title: Performance Testing
permalink: /guides/testing/performance
---

[WIP]

# Performance testing

This guide expresses some general ideas about how we think about the term performance testing.
It's important to express the nomenclature as load testing is simply an umberella term that can be used to describe any kind of testing involving some deliberate requests.

## Types

We have a few main types as we walk ourselves up the triangle. Starting from the bottom, we have:

within the *codebase*
- Unit benchmarks
- Pallet benchmarks

within the *network*
- Load testing
- Capacity testing
- Soak testing
- Stress testing

So what do the types mean to us?

## Within the codebase

Within the codebase simply means that we do not need any external tools, we have tools in our arsenal that will allow us to test natively.

[Rust tools]

[Substrate tools]

### Unit Benchmarks

Our most granular level of benchmarking. 
This type of benchmarking is usually used for complex, small units of the code base, such as:
- hand-written algorithms
- comparing algorithms

### Pallet Benchmarks

Pallet benchmarking relates to substrate, and answers some of our most important questions around block weighting(weight link) and how much a call(link call) will cost. 

This is kind of a integration-like benchmark test in that it tests a black box of the system, largely due to the fact that call's are generally database reads, network calls and such.

## Within the network

Within the network is simply anything external to the codebase and we would need an external tool to test it.

What do we want from tools:
- reproducable
- true
- as code

[Drill](sdkfjh)

### Load testing

Load testing is the most basic form of performance testing, it also has a fair amount of metrics that it can be applied to, for example:
- latency(L99, L95, etc) under 50 concurrent requests
- throughput under 10 users
- how many errors do we get?(success rate)
- does it die?(basic questions)

Generally load testing is something done at a whim to answer a bespoke question, it does not answer all the things we would normally want to know about a system.
It might be a simple api endpoint, or a small subset of the system such as a resource.

### Scalability testing

Scalability testing is to understand what the maximum amount of requests/users can be handled by a system under some set parameters.

This sort of testing tends to feed directly into scaling parameters, instancing schemas and sizes of resources.

Some example questions might be: 

- with 4 services running, how many users can we support?
- with 10k users, what do we need to scale to?
- when does our load balancing strategy fail?
- when should we scale up?
- when should we scale out?

As you can see, some metrics for scalability testing are not directly related to load testing. It usually is:
- users
- error rate
- basic questions
- service cpu
- service memory
- network bandwidth

### Soak testing

Soak testing is quite like scalability testing, although performed under a time. 
Generally the main question is: does it fail? 
Therefore the key to getting a good test is drilling into the definition of failure, things like acceptable error rate at certain times might be applicable.

Some example questions might be:
- If we have 300 users with a derivative of 5% and the test is run for a week. Do we have an error rate of more than 0.5%? 
- If we have 30 users and on a certain day we have a peak of 5000 users, can we serve 95% of the users?

As you can see, the questions tend to be quite specific and around time, note that the time is a parameter.

Also take note that we are also not simply sending a straight amount of users, we are sending a derivative of users. 
It's perfectly reasonable to simply send 30 users for 30 days however.

It generally helps feed into scaling policies and answer some real world questions.

### Stress testing

Stress testing is a form of load testing that is simply trying to break your system. The most common practice is adding additional users over some period of time until it dies. Usually this will stretch the scaling policy of the system and lead to failure.

Cost is an important consideration, so stress tests are generally quite short, and not in a production environment. Although not impossible.

It does answer a very important question, what can we do under what maximum parameters and how long does it take to fail?

This is usually what stakeholders or budget coordinators are the most interested in.

### Footnote on performance testing types

They are all quite similar, and there are no held fast rules. But it is important to use the right nomenclature for what you mean.

## Metrics

Common metrics we want out of performance testing are generally unanimous amongst the industry.

### Users

Users, or requests, simply refers to the number of concurrent requests that are being made to the system. It could be:

- sending api calls
- sending multiple api calls, such as authenticating, creating a resource, etc
- following a flow of requests
- querying caches


### Latency

Latency is simply just how long it takes to get a response from the system. We generally use the [L99](https://en.wikipedia.org/wiki/99_percentile) and [L95](https://en.wikipedia.org/wiki/95_percentile) as common metrics.

### System

System metrics are usually CPU %, RAM, IO and network bandwidth.

### Error Rate

Error rate is the percentage of requests that fail, or sometimes the raw number of requests that fail.
It could also be the amount of times a system is killed, or restarted, number of times database operations fail, etc.

Generally anything exceptional that might happen to the system is counted in an error rate.

### Basic questions

The most basic question is "does it die?" and commonly refers to an intrinsic error rate.