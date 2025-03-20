# Installation & Usage

> **IMPORTANT: If your operating system is Windows, you must run VSCode using** [**WSL**](https://learn.microsoft.com/en-us/windows/wsl/)**.**

1. In VSCode, open the "Extensions" tab
2. Search and install "Aderyn"
3. Open the "Aderyn: Welcome" page (if it hasn't automatically opened)
4. Done!

Aderyn works seamlessly on commonly recognized project structures, i.e., when a `foundry.toml` or `hardhat.config.js` is found in the workspace's root.

In addition, you can configure how Aderyn analyzes your project by creating an `aderyn.toml` file in the project root. This is important when running Aderyn on a project that does not use a well-known Solidity development framework like Foundry or Hardhat.\
\
To create this file, open the VSCode command palette and hit `Aderyn: Intitialize Config` . For instructions on how to configure aderyn.toml, visit [aderyn.toml-configuration.md](aderyn.toml-configuration.md "mention")

