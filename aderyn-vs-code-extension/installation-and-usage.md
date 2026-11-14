# Installation & Usage

{% hint style="warning" %}
**The Aderyn VS Code extension is retired and is no longer maintained.** Its Marketplace listing has been unpublished and its GitHub VSIX downloads withdrawn. Delisting does not uninstall existing copies or guarantee that every cached or registry download is unavailable. See the [retirement notice](https://aderyn.cyfrin.io/retirement) for the current status.
{% endhint %}

### Remove an existing installation

1. Open the **Extensions** view in VS Code and find the installed **Aderyn** extension (`Cyfrin.aderyn`).
2. Choose **Uninstall**, then reload VS Code if prompted.
3. Check any other VS Code profiles or remote environments where you installed it.

Uninstalling the extension does not necessarily remove a separately installed Aderyn CLI. Follow the [CLI removal guidance](https://aderyn.cyfrin.io/retirement) as needed.

### Historical configuration reference

The following configuration information is retained for reference. It does not imply ongoing maintenance or working installation and update services.

Aderyn works seamlessly on commonly recognized project structures, i.e., when a `foundry.toml` or `hardhat.config.js` is found in the workspace's root.

In addition, you can configure how Aderyn analyzes your project by creating an `aderyn.toml` file in the project root. This is important when running Aderyn on a project that does not use a well-known Solidity development framework like Foundry or Hardhat.\
\
To create this file, open the VSCode command palette and hit `Aderyn: Intitialize Config` . For instructions on how to configure aderyn.toml, visit [using-the-config-file-aderyn.toml.md](../project-configuration/using-the-config-file-aderyn.toml.md "mention")

