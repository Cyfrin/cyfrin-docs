# Installation

> **NOTE** Windows users must have WSL installed

#### Using Cyfrinup

**Cyfrinup** simplifies the installation and management of Cyfrin tools.

Follow the instructions to install [here](https://github.com/Cyfrin/up).

Run `aderyn --version` to check the installation.

**Upgrade older versions by (re)running: `cyfrinup`**

***

#### Using Homebrew

```sh
brew install cyfrin/tap/aderyn
```

**Upgrade older versions by running: `brew upgrade cyfrin/tap/aderyn`**

***

#### Using npm

```sh
npm install @cyfrin/aderyn -g
```

**Upgrade older versions by (re)running: `npm install @cyfrin/aderyn -g`**

***

If you are installing with Homebrew or npm, ensure that the correct version of Aderyn in your path comes from either the Homebrew or npm global packages directory. If an older version exists at `~/.cyfrin/bin/aderyn`, remove it using `rm -f ~/.cyfrin/bin/aderyn`, as this is no longer the default installation location.

