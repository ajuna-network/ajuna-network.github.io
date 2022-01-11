---
layout: default
title: Substrate Development
permalink: /guides/development/substrate
---

[crates-io]: https://crates.io/
[ipfs]: https://ipfs.io/
[parachain-devops-best-practices]: https://gist.github.com/lovelaced/cddc1c7234b883ee37e71cf4a1d63cac
[rust-docs-collections-performances]: https://doc.rust-lang.org/std/collections/index.html#performance
[rust-rocksdb]: https://github.com/rust-rocksdb/rust-rocksdb
[substrate-docs]: https://docs.substrate.io/
[substrate-docs-getting-started]: https://docs.substrate.io/v3/getting-started/overview/
[substrate-docs-how-to-guides]: https://docs.substrate.io/how-to-guides/v3/
[substrate-docs-tutorials]: https://docs.substrate.io/tutorials/v3/
[substrate-docs-rustdocs]: https://docs.substrate.io/rustdocs/
[substrate-docs-storage]: https://docs.substrate.io/v3/runtime/storage/
[substrate-docs-benchmarking]: https://docs.substrate.io/v3/runtime/benchmarking/#best-practices-and-common-patterns
[substrate-monthly-releases]: https://github.com/paritytech/substrate/releases?q=monthly-&expanded=true

# Substrate Development

The best resources in Substrate development are the official docs:

- [Substrate Developer Hub][substrate-docs]
  - [Docs][substrate-docs-getting-started] - concepts and high-level overview of ideas
  - [How-to Guides][substrate-docs-how-to-guides] - more in-depth, hands-on guide and recipes on developing in Substrate
  - [Tutorials][substrate-docs-tutorials] - code exercises and walkthrough on various use cases of Substrate
- [Substrate Rust Docs][substrate-docs-rustdocs]

### Crate Naming Convention

Follow the convention mentioned in [Rust Development](rust.md#crate-naming-convention) with exception for runtime modules (or pallets).

For pallets, prefixing with `ajuna-pallet-*` is appropriate.

### Managing Substrate Dependencies

Recommended is to peg our upstream dependencies at [monthly snapshot releases][substrate-monthly-releases] with a dedicated time slot each month for upgrading.

#### Versioned, monthly or latest releases - which one to use

Versioned released are infrequent in Substrate which often leads to a simple upgrade task requiring lots of effort.
Other options include:

- pointing directly to the latest `master` branch, which means
  - our maintenance effort is increased substantially due to breaking changes
  - our codebase has the latest and greatest changes
- pointing to a specific commit on `master` branch, which means
  - our maintenance effort can be managed
  - our codebase has the latest and greatest changes up until the commit
  - it's difficult to understand what changes are included up until that particular commit

A nice trade-off between maintainability vs. latest tech is provided via [monthly snapshot releases][substrate-monthly-releases], where we can dedicate a time slot for upgrading every month.
A changelog for each monthly release is also provided to help us understand its associated changes.

### Runtime Development

Our nodes can be thought of as distributed state machines with shared resources.
These resources are tied to knowing how busy our network is and contribute to increasing or decreasing transaction fees.
Hence pallets must be developed with optimization in mind towards:

- disk I/O
- memory usage
- computation

#### Disk I/O

Generally we aim to minimize the amount of storage a pallet uses _by storing consensus critical information only_.
If we don't have logic to read a particular data, it probably means we don't need to store it on chain.

Substrate is coupled with a variant of Merkle Patricia tree and key-value DB (e.g, [RocksDB][rust-rocksdb]), which means we don't have to optimize the underlying storage operations.

We suggest the following to optimize storage items:

- verify upfront and write last to ensure no partial data are persisted when an extrinsic fails
- combine commonly accessed values together into a `struct`, rather than dispersing them across multiple storage items
  - this will create fewer nodes in the underlying tree structure to keep `O(log N)` low
  - we can update multiple values with a single `read` and `write`
- use `xxHash` over `BLAKE2` hashing algorithm for its hashing speed
  - NOTE: users won't be allowed to modify key prefixes so it's safe to use it
- for storing lists, consider using `frame_support::BoundedVec` to ensure we don't run into iterating over a massive list
- for storing large data, consider storing hash pointer or CID to [IPFS][ipfs]

See [Storage][substrate-docs-storage] for more info.

#### Memory Usage

Related to [Disk I/O](#disk-io), we should consider using the smallest data types required for the job.

#### Computation

See [microbenchmarks](../testing/performance.md#microbenchmarks) for measuring a piece of code.

#### Further Considerations

- [Benchmarking best practices][substrate-docs-benchmarking]
- [Parachain DevOps best practices][parachain-devops-best-practices]
