---
layout: default
title: Prerequisite
permalink: /development/prerequisite
---

[homebrew-rust-formula]: https://formulae.brew.sh/formula/rust/
[openssl]: https://www.openssl.org/
[rust]: https://www.rust-lang.org/
[rust-install]: https://www.rust-lang.org/tools/install/
[rust-analyzer]: https://rust-analyzer.github.io/
[rust-language-server]: https://github.com/rust-lang/rls
[substrate]: https://substrate.io/
[substrate-docs-install-build-deps]: https://docs.substrate.io/v3/getting-started/installation/#1-build-dependencies
[toml-wiki-editor-support]: https://github.com/toml-lang/toml/wiki#editor-support
[vscode]: https://code.visualstudio.com/
[vscode-even-better-toml]: https://marketplace.visualstudio.com/items?itemName=tamasfe.even-better-toml
[vscode-rls]: https://marketplace.visualstudio.com/items?itemName=rust-lang.rust
[vscode-rust-analyzer]: https://marketplace.visualstudio.com/items?itemName=matklad.rust-analyzer
[vscode-spell-checker]: https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker
[web-assembly]: https://webassembly.org/

# Prerequisite

Ajuna Network is built using the [Substrate][substrate] framework and relies heavily on [Rust][rust] as the programming language.
Any level of familiarity with either of the subjects will be useful but is _not_ required as we can provide support on filling knowledge gaps on those subjects.

To start developing on Ajuna Network, we recommend reading through our suggestions below.

Also see [Tools and Extensions](tools-and-extensions.md) for more recommendations.

### Build Dependencies

The main binary required to build our blockchain project is [OpenSSL][openssl].
Follow these [instructions][substrate-docs-install-build-deps] to install it for your operating system.

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

Run the below command to install necessary components, only available via `nightly` releases, to target Wasm.

```sh
rustup update nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
```

### IDE

You can choose any IDEs as long as it supports either the official [Rust Language Server][rust-language-server] (RLS) or the alternative [rust-analyzer][rust-analyzer].
However we recommend the following extensions (or plugins) for your IDE of choice.
The examples below are given based on [VS Code][vscode] but any tools that serve similar purposes for your IDE are acceptable.

- [RLS][vscode-rls] or [rust-analyzer][vscode-rust-analyzer]
  - Make sure automatic execution of `cargo fmt` is enabled
- [Code Spell Checker][vscode-spell-checker]
  - Spelling consistencies help us search through our codebase efficiently
  - Make sure American English spelling is enabled to align with the [Substrate][substrate] codebase to help us search across both codebase efficiently
- [Even Better TOML][vscode-even-better-toml]
  - This extension is the only one that supports both syntax highlighting and formatting as well as being [mentioned by the official TOML][toml-wiki-editor-support]
  - Make sure alphabetical ordering of keys is enabled

Finally make sure these are set in `settings.json`:

```json
{
  "[rust]": {
    "editor.defaultFormatter": "matklad.rust-analyzer"
  },
  "cSpell.language": "en",
  "editor.formatOnSave": true,
  "evenBetterToml.formatter.reorderKeys": true,
  "files.insertFinalNewline": true,
  "files.trimTrailingWhitespace": true
}
```
