---
layout: default
title: Prerequisite
permalink: /guides/prerequisite
---

# Prerequisite

Ajuna Network is built using the [Substrate][substrate] framework and relies heavily on [Rust][rust] as the programming language.
Any level of familiarity with either of the subjects will be useful but is _not_ required as we can provide support on filling knowledge gaps on those subjects.

To start developing on Ajuna Network, we recommend reading through our suggestions below.

### Rust

Rust can be installed using package managers such as [Homebrew][homebrew-rust-formula] but we recommend following the [official way][rust-install] as shown below.

```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Once the installation finishes, Rust's toolchain manager `rustup` should be available. Run the following to make sure the `stable` release channel is referenced by default and update to the latest `stable` releases.

```sh
rustup default stable && rustup update
```

[Substrate][substrate] uses [WebAssembly][web-assembly] to allow runtime modules to be compiled down to Wasm blobs, which can then be shared across a compatible Substrate-based blockchain network to achieve forkless upgrades of the chain. To do so, we need to be able to target Wasm binaries when building our project.

Run the below command to install necessary toolchain to target Wasm only available via `nightly` releases.

```sh
rustup update nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
```

<!-- https://docs.substrate.io/v3/getting-started/installation/#1-build-dependencies -->

[homebrew-rust-formula]: https://formulae.brew.sh/formula/rust/
[rust]: https://www.rust-lang.org/
[rust-install]: https://www.rust-lang.org/tools/install/
[substrate]: https://substrate.io/
[web-assembly]: https://webassembly.org/

### IDE

TODO:

- suggested IDEs
- suggested extensions / plugins

### Docker

TODO
