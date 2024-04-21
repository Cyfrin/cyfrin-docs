# Installation

### Prerequisites

Before installing Aderyn, ensure you have the following:

* **Rust**: Aderyn is built in Rust. Before running, you must install Rust and Cargo (Rust's package manager). If you haven't installed Rust yet, follow the instructions on the [official Rust website](https://www.rust-lang.org/learn/get-started).

{% hint style="info" %}
Aderyn currently only supports Foundry-based projects. If you're using Hardhat, please refer to our GitHub repository for information on [how to contribute](https://github.com/Cyfrin/aderyn/blob/dev/CONTRIBUTING.md).
{% endhint %}

**Suggested VSCode extensions:**

* [rust-analyzer](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer) - Rust language support for Visual Studio Code
* [Rust Syntax](https://marketplace.visualstudio.com/items?itemName=dustypomerleau.rust-syntax) - Improved Rust syntax highlighting

***

### Installing Aderyn

**Step 1: Install Aderyn using cargo**

Aderyn is currently installed using Cargo, Rust's package manager. Open your command line interface and run the following command:

```bash
cargo install aderyn
```

This command downloads and installs the Aderyn package.

**Step 2: Verify installation**

After the installation, you can verify that Aderyn is correctly installed by checking its version. In your command line, execute:

```bash
aderyn --version
```

This command should return the installed version of Aderyn, confirming that the installation was successful.

**Step 3: Update PATH (if necessary)**

If you're unable to run the `aderyn` after installation, you may need to add Cargo's bin directory to your PATH. The exact instructions can vary based on your operating system. Typically, it involves adding `~/.cargo/bin` to your PATH in your shell profile script (like `.bashrc` or `.zshrc`).

**Step 4: Future Updates**

To update Aderyn to the latest version, you can run the install command again:

```bash
cargo install aderyn
```

Cargo will replace the existing version with the latest one.

Now that you have Aderyn installed let's see [how to run it to find vulnerabilities in your codebase](quickstart.md).



### Run Aderyn Using DOcker

You can run Aderyn from a Docker container.

Build the image:

```sh
  docker build -t aderyn .
```

`/path/to/project/root` should be the path to your Foundry or Hardhat project root directory and it will be mounted to `/share` in the container.

Run Aderyn:

```sh
  docker run -v /path/to/project/root/:/share aderyn
```

Run with flags:

```sh
  docker run -v /path/to/project/root/:/share aderyn -h
```
