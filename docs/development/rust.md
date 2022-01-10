---
layout: default
title: Rust Development
permalink: /guides/development/rust
---

[api-guidelines-discussion-29]: https://github.com/rust-lang/api-guidelines/discussions/29
[crates-io]: https://crates.io/
[design-patterns]: https://rust-unofficial.github.io/patterns/patterns/index.html
[destructuring]: https://doc.rust-lang.org/rust-by-example/flow_control/match/destructuring.html
[if-let]: https://doc.rust-lang.org/rust-by-example/flow_control/if_let.html
[kiss]: https://en.wikipedia.org/wiki/KISS_principle
[software-design-principles]: https://en.wikipedia.org/wiki/List_of_software_development_philosophies#Rules_of_thumb,_laws,_guidelines_and_principles

# Rust Development

### Crate Naming Convention

There isn't a standard naming convention for crates [see this discussion][api-guidelines-discussion-29] however we recommend names in hyphen-delimited kebab-case with prefix `ajuna-*`, where appropriate.

Also consider using:

- nesting or hierarchy as a way to group packages together
- suffixes to differentiate between

For example,

```
ajuna-dot4-engine
ajuna-dot4-client
ajuna-dot4-deployment
```

When publishing to [crates.io][crates-io], we want to double-check on the names as they are immutable.

### Repo Naming Convention

The only standard we enforce in naming Rust-based repositories is using kebab-case.
Most names should be acceptable as long as the names reflect their intended purposes.

### Design Principles

There are numerous [software design principles][software-design-principles] available to us.
One that we strongly feel affinity towards is the [KISS principle][kiss].

> Perfection is achieved, not when there is nothing more to add, but when there is nothing left to take away.

### Design Patterns

Design patterns are something we aren't stressing over at the moment.

Once we identify common problems we will reflect on our codebase to enforce patterns where necessary.

However if you're still interested, here is [a comprehensive list][design-patterns].

### Idioms

- thinking in terms of expressions:

  ```rust
  let x = {
    let intermediate_1 = 1;
    let intermediate_2 = 2;
    x_1 + x_2
  }
  ```

- following Rust's convention to name constructors `new`

  ```rust
  struct Block {
    block_number: u64
  }

  impl Block {
    fn new(block_number: u64) -> Self {
      Block { block_number }
    }
  }
  ```

- following Rust's convention to name getters same as fields they are accessing

  ```rust
  struct Coordinate {
    x: i32,
    y: i32,
  }

  impl Coordinate {
    fn x(&self) -> &i32 {
      &self.x
    }
    fn y(&self) -> &i32 {
      &self.y
    }
  }
  ```

### Best Practices

Most best practices will be suggested by simply running `clippy` over the codebase.
However some of the noteworthy ones are:

- using [destructure][destructuring] to avoid unnecessary nesting
- using [if let][if-let] expressions to avoid unnecessary pattern matching
- using `unsafe` blocks, unless they are for FFI
- keeping scope of variables to where they are used
- most importantly, keep it simple 🙂

### Bad Practices

We want to avoid:

- bypassing compiler warnings with attributes such as:
  - `#![deny(warnings)]`
  - `#![allow(dead_code)]`
- bypassing linting and formatting of code with attributes such as:
  - `#![allow(clippy::all)]`
  - `#![rustfmt::skip]`
- abusing `clone` to satisfy borrow checker
