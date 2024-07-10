# Installation

**Suggested VSCode extensions:**

* [rust-analyzer](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer) - Rust language support for Visual Studio Code
* [Rust Syntax](https://marketplace.visualstudio.com/items?itemName=dustypomerleau.rust-syntax) - Improved Rust syntax highlighting

***

### Installing Aderyn

#### **Step 1: Install Cyfrinup**

Cyfrinup is a CLI tool that simplifies the installation and management of Cyfrin tools. To install Cyfrinup, run the following command in your terminal:

```
curl -L https://raw.githubusercontent.com/Cyfrin/aderyn/dev/cyfrinup/install | bash
```

#### **Step 2: Update Path**

The installer will prompt you to run a `source` command. Either run this command or reload your terminal.

#### **Step 3: Install Aderyn using Cyfrinup**

After installing Cyfrinup, you can use it to install Aderyn. Run the following command in your terminal:

```
cyfrinup
```

#### **Step 4: Verify installation**

```
aderyn --version
```

#### **Future Updates**

To update Aderyn to the latest version, you can run the cyfrinup:

```
cyfrinup
```

Cyfrinup will replace the existing version with the latest one.

Now that you have Aderyn installed let's see [how to run it to find vulnerabilities in your codebase](quickstart.md).

### Run Aderyn Using Docker

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
