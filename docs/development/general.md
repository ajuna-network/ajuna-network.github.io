---
layout: default
title: General Development
permalink: /guides/development/general
---

[conventional-commits]: https://www.conventionalcommits.org/en/v1.0.0/
[jira]: https://ajunanetwork.atlassian.net/jira
[trunk-based-development]: https://trunkbaseddevelopment.com/

# General Development

Here is a list of conventions and styles we follow to help us reduce cognitive load on trivial stuff.

### Development Style

We follow the popular [trunk-based development][trunk-based-development] style where we regard `master` branch as the single source of truth and encourage everyone to checkout from.

We will manage releases by creating tags from `master` branch such that there is no burden of maintaining separate release branches.

We will also merge pull requests by either _squashing_, for changes relating to one particular scope, or _rebasing_, for changes across multiple scopes in order to avoid creating merge commits.

Amending commits or rebasing interactively from your working branch is encouraged, and therefore force pushing is also encouraged from your branch.

### Branch Naming Convention

Since we will be working on tasks captured in [Jira][jira], we can use Jira ticket numbers in naming our branches.

Also important to consider are as follows:

- prefix of your first and last name initials to avoid name conflicts and help others identify you for communication
- suffix of a short description of associated task to reduce having to open the associated Jira ticket links

Our suggestion is the following naming convention.

```
<initials>/<JIRA-TICKET-NUMBER>-<short-description>
```

An example branch name for a developer named, _Marty McFly_, working on Jira ticket, _ABC-12_, would be `mm/ABC-12-recharge-the-flux-capacitor`.

### Commit Message Convention

We follow the [Conventional Commits][conventional-commits] style of writing commit messages.
We rely on the consistency of following this style to trigger automated builds and releases as well as changelog generation.

### Technical Debts

If you're in a situation where a technical debt has to be created on the fly, it must be captured as both:

- a Jira task labelled with `Tech Debt`, and
- a `TODO` comment with reference to the ticket number of the task created

Follow the below naming convention.

```rust
// TODO: DEBT-123 this function must be deleted after release
fn create_tech_debt() { unimplemented!() }
```
