---
layout: default
title: Tools & Extensions
permalink: /guides/development/tools-and-extensions
---

[vscode]: https://code.visualstudio.com/
[vscode-insiders]: https://code.visualstudio.com/insiders/
[rust-analyzer]: https://marketplace.visualstudio.com/items?itemName=matklad.rust-analyzer
[crates]: https://marketplace.visualstudio.com/items?itemName=serayuzgur.crates
[podman]: https://podman.io/
[docker]: docker.io
[docker-extension]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker
[gitlens]: https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens
[conventional-commits]: https://www.conventionalcommits.org/en/v1.0.0/
[conventional-commits-extension]: https://marketplace.visualstudio.com/items?itemName=vivaxy.vscode-conventional-commits
[gitkraken]: https://www.gitkraken.com/
[clion]: https://www.jetbrains.com/
[github-copilot]: https://copilot.github.com/
[tabnine]: https://www.tabnine.com/
[remote-containers]: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers
[dev-container]: https://code.visualstudio.com/docs/remote/devcontainerjson-reference
[substrate]: https://marketplace.visualstudio.com/items?itemName=paritytech.vscode-substrate
[rustfmt]: https://github.com/rust-lang/rustfmt
[clippy]: https://github.com/rust-lang/rust-clippy
[better-toml]: https://marketplace.visualstudio.com/items?itemName=bungcip.better-toml
[even-better-toml]: https://marketplace.visualstudio.com/items?itemName=tamasfe.even-better-toml
# Tools & Extensions

This is not prescriptive but just a demonstration of some of the tools we use within the team.

# IDE

Among the team, it depends on the use case, the usual players are [VSCode][vscode], [CLion][clion], although CLion is lacking when it comes to Substrate with a load of false positives, e.g:
- [E0277](https://github.com/intellij-rust/intellij-rust/issues?q=is%3Aissue+is%3Aopen+E0277)
- [E0308](https://github.com/intellij-rust/intellij-rust/issues?q=is%3Aissue+is%3Aopen+E0308)

Until then, some of the team have moved to [VSCode][vscode-insiders] and [Rust Analyzer][rust-analyzer].

## Auto-Completion

Some of the team use additional auto completion tools like [Github Copilot][github-copilot](currently free trial) and [TabNine][tabnine].

# Git

To follow [Conventional Commits][conventional-commits], we use the [extension][conventional-commits-extension]. Or you can also set a default commit msg template like so:

- Make a file somewhere, in this case, `git-commit-msg-template`:
    ```
    <type>(optional scope): <description>


    [optional body]

    [optional footer]
    ```
- git config --global commit.template $HOME/git-commit-msg-template

This will now be a global default.

We also use the [Gitlens][gitlens] extension. However, this has been acquired by [GitKraken][gitkraken], so it will likely become proprietary in the future. Some of us also use [GitKraken][gitkraken] for complex rebases and such.


# Rust

For rust, there are a few extensions that the team uses.

For viewing dependencies, we use [crates][crates]. This shows us potential upgrades and such.

For linting, we use [Clippy][clippy] and for formatting, we use [RustFmt][rustfmt].

For toml editing, there is [Better TOML][better-toml] and [Even Better TOML][even-better-toml].

# Substrate

The team also uses a [Substrate][substrate] extension for VSCode.

# Containerisation

Some of the team use [Docker][docker] and [Docker Extension][docker-extension] for containerisation. Some of the team use [Podman][podman] for containerization and daemonless OCI containers.

There is also the [Remote: Containers][remote-containers] extension for VSCode, this is a great tool that can make use of [Dev Containers][dev-container]. This is a great tool for our dev environment, as the Substrate team also uses it.