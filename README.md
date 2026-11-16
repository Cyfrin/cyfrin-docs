---
description: >-
  /aˈdɛrɪn/ - Welsh (noun) - Bird. A member of the class of animals Aves in the
  phylum Chordata.
---

# What is Aderyn?

{% hint style="warning" %}
**Aderyn is retired and is no longer maintained.** These legacy docs remain available for reference. See the [retirement notice and removal guidance](https://aderyn.cyfrin.io/retirement) and the [retained Aderyn documentation](https://aderyn.cyfrin.io/).
{% endhint %}

Aderyn is an open-source, Rust-based Solidity smart contract static analyzer originally designed to help protocol engineers and security researchers find vulnerabilities in Solidity codebases. The features and examples below describe its historical behavior.

Thanks to its collection of static vulnerability [detectors](internals/what-is-a-detector.md), running Cyfrin Aderyn on your Solidity codebase will **highlight all the potential vulnerabilities**, drastically reducing the potential for unknown issues in your Solidity code and giving you the **time to focus on more complex problems**.

Built using **Rust**, Aderyn i**ntegrates seamlessly into small and enterprise-level development workflows**, offering lighting-fast command-line functionality and a framework to build [custom detectors](/broken/pages/Ckl5FeyKmDSmOpk3Z0x2) to adapt to your codebase.

Aderyn does multiple things, but at its core, it will help you:

**1. Identify Solidity Smart contract vulnerabilities:** Solidity Developers and Security Auditors use Cyfrin Aderyn to **identify potential vulnerabilities** in Solidity code and highlight parts of the codebase for further investigation.

2\. **Supports** **Building custom detectors to suit your needs:** Protocols and security researchers use the Cyfrin Aderyn detectors framework to [build custom vulnerability detectors](internals/detectors-quickstart/) for any codebase.

3\. **Identify known issues and protect your value:** Competitive auditing platforms can use Cyfrin Aderyn to detect and filter out known issues inside protocol codebases, protecting customers' and auditors' time and value.

**You can check out the Cyfrin Aderyn repo on** [**GitHub**](https://github.com/Cyfrin/aderyn/tree/dev)**.**

***

### Cyfrin Aderyn Key Features

1. **Static Analysis of Solidity Smart Contracts**: Aderyn excels in parsing and analyzing Solidity smart contracts, providing insights into potential security risks and inefficiencies. Jump to [Aderyn quickstart](https://cyfrin.gitbook.io/cyfrin-docs/aderyn-cli/quickstart).
2. **Adapt Aderyn to any codebase**:  Aderyn allows developers to [create custom detectors](internals/detectors-quickstart/) to analyze and find specific code-based vulnerabilities.&#x20;
3. **Command Line Interface**: Aderyn offers a developer-friendly CLI to customize its settings and your Solidity smart contracts analysis and reports.
4. **Analyse only what matters**: Aderyn allows specifying particular contracts to be analyzed or excluded, giving users control over the scope of the analysis.
5. **Full control over your reports**: The analysis results can be outputted in different formats, including Markdown and JSON, catering to different needs, such as human-readable reports or CI (Continuous Integration) pipeline integration.
6. **Lighting fast execution**: Written in Rust, Aderyn keeps its analysis times under the second.

***

### Historical Use Cases

Aderyn's documented use cases included:

* **Pre-audit Analysis**: Developers can use Aderyn to identify and address critical, high, and medium-severity issues in smart contracts before sending them for formal audits.
* **Automated Testing in CI Pipelines**: Integrating Aderyn into CI pipelines allows automated scanning of contracts with each build, ensuring continuous security.
* **Smart Contract Development and Debugging**: Developers can use Aderyn during the development phase to catch issues early in the development lifecycle.
* **Custom Security Analysis**: By creating custom detectors, users can tailor the analysis to specific needs or concerns unique to their projects.
* **Competitive audit finding exclusion list**: Aderyn could identify findings to list as "known issues" before an audit competition.

***

### Source and maintenance status

Aderyn's source history remains available on [GitHub](https://github.com/Cyfrin/aderyn) for reference and reproducibility. Cyfrin no longer maintains Aderyn or provides new releases, fixes or feature updates.

The detector framework and other technical material in these docs are retained as historical reference. For the current retirement status and guidance for existing users, read the [retirement notice](https://aderyn.cyfrin.io/retirement).
