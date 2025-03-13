# Quickstart

Aderyn uses a series of [detectors](detectors-quickstart/) that, given a set of Solidity smart contracts within a directory, analyze the smart contracts Abstract Syntax Tree ([AST](what-is-an-ast.md)) to find vulnerability patterns and report them in an easy-to-consume markdown document.

In this article, you will learn how to get started using Aderyn to analyze your Solidity codebase and generate a report on its vulnerabilities.

{% embed url="https://youtu.be/j9DxOIa6phE" %}

### Prerequisites

Before installing Aderyn, ensure you have the following:

* **Aderyn installed:** Follow this guide to learn [how to install Aderyn](installation.md) on your system.

**Suggested VSCode extensions:**

* [rust-analyzer](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer) - Rust language support for Visual Studio Code
* [Rust Syntax](https://marketplace.visualstudio.com/items?itemName=dustypomerleau.rust-syntax) - Improved Rust syntax highlighting

***

### Running Aderyn to analyse your codebase

Once [Aderyn is installed on your system](installation.md), you can run it against any Solidity codebase to find vulnerabilities in your code.

In this example, we will use the [aderyn-contracts-playground repository](https://github.com/Cyfrin/aderyn-contracts-playground).

{% hint style="info" %}
This example codebase uses Foundry. Please [install Foundry](https://book.getfoundry.sh/getting-started/installation) as a prerequisite to working with this example repository.
{% endhint %}

You can follow along by cloning it to your system.

```
git clone https://github.com/Cyfrin/aderyn-contracts-playground.git
```

Navigate inside the repository:

```
cd aderyn-contracts-playground
```

We usually use several smart contracts and tests to try new [detectors](what-is-a-detector.md). Install dependencies and build the contracts by running:

```
forge build
```

Once your smart contracts have been successfully compiled, run Aderyn using the following command:

```bash
aderyn [OPTIONS] path/to/your/project
```

Replace `[OPTIONS]` with specific [command-line arguments ](../cli-options.md)as needed.

**What happens when you call `aderyn?`**

* Search for all Solidity files within the directory structure
* Compile the Solidity files and load their ASTs into its [`WorkspaceContext`](detectors-quickstart/detectors-api-reference/workspacecontext.md)
* For each available [detector](detectors-quickstart/), call [`detect`](detectors-quickstart/detectors-api-reference/detect.md) and pass in the [`WorkspaceContext`](detectors-quickstart/detectors-api-reference/workspacecontext.md)

Your codebase's full markdown security report will be generated for you now.

***

### Generating the Aderyn security report

When executed, Aderyn will generate a full security report of your Solidity code base. You can find the standard here: [https://github.com/Cyfrin/aderyn/blob/dev/reports/report.md](https://github.com/Cyfrin/aderyn/blob/dev/reports/report.md)

You can direct the output to a specific file or change the format to JSON for integration with other tools:

```bash
aderyn --output report.md
```

```
aderyn --output report.json
```

Inside the generated report, you will find:

* A summary of your codebase properties (nsloc, complexity, etc.)
* A summary of the issues and their severity divided by Highs and Lows.
* A list of the issues with descriptions and links to the line of code where the vulnerability was found

***

### Modify or create a custom detector

Cyfrin Aderyn gives engineers and security an easy-to-implement framework to develop custom static analysis detectors that can **adapt to any codebase** or use case. You can learn more about creating[ a custom Cyfrin Aderyn detector](detectors-quickstart/) on the related documentation page.
