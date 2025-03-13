---
description: >-
  /aˈdɛrɪn/ - Welsh (noun) - Bird. A member of the class of animals Aves in the
  phylum Chordata.
---

# What is Aderyn?

Aderyn is an open-source, public-good developer tool. It is a Rust-based solidity smart contract static analyzer designed to help protocol engineers and security researchers find vulnerabilities in Solidity code bases.

Thanks to its collection of static vulnerability [detectors](what-is-a-detector.md), running Cyfrin Aderyn on your Solidity codebase will **highlight all the potential vulnerabilities**, drastically reducing the potential for unknown issues in your Solidity code and giving you the **time to focus on more complex problems**.

Built using **Rust**, Aderyn i**ntegrates seamlessly into small and enterprise-level development workflows**, offering lighting-fast command-line functionality and a framework to build [custom detectors](broken-reference) to adapt to your codebase.

Aderyn does multiple things, but at its core, it will help you:

**1. Identify Solidity Smart contract vulnerabilities:** Solidity Developers and Security Auditors use Cyfrin Aderyn to **identify potential vulnerabilities** in Solidity code and highlight parts of the codebase for further investigation.

2\. **Supports** **Building custom detectors to suit your needs:** Protocols and security researchers use the Cyfrin Aderyn detectors framework to [build custom vulnerability detectors](detectors-quickstart/) for any codebase.

3\. **Identify known issues and protect your value:** Competitive auditing platforms can use Cyfrin Aderyn to detect and filter out known issues inside protocol codebases, protecting customers' and auditors' time and value.

**You can check out the Cyfrin Aderyn repo on** [**GitHub**](https://github.com/Cyfrin/aderyn/tree/dev)**.**

***

### Cyfrin Aderyn Key Features

1. **Static Analysis of Solidity Smart Contracts**: Aderyn excels in parsing and [analyzing Solidity smart contracts](quickstart.md), providing insights into potential security risks and inefficiencies.
2. **Adapt Aderyn to any codebase**:  Aderyn allows developers to [create custom detectors](broken-reference) to analyze and find specific code-based vulnerabilities.&#x20;
3. **Command Line Interface**: Aderyn offers a developer-friendly CLI to customize its settings and your Solidity smart contracts analysis and reports.
4. **Analyse only what matters**: Aderyn allows specifying particular contracts to be analyzed or excluded, giving users control over the scope of the analysis.
5. **Full control over your reports**: The analysis results can be outputted in different formats, including Markdown and JSON, catering to different needs, such as human-readable reports or CI (Continuous Integration) pipeline integration.
6. **Lighting fast execution**: Written in Rust, Aderyn keeps its analysis times under the second.

***

### Use Cases

Aderyn is versatile and can be used in various scenarios, such as:

* **Pre-audit Analysis**: Developers can use Aderyn to identify and address critical, high, and medium-severity issues in smart contracts before sending them for formal audits.
* **Automated Testing in CI Pipelines**: Integrating Aderyn into CI pipelines allows automated scanning of contracts with each build, ensuring continuous security.
* **Smart Contract Development and Debugging**: Developers can use Aderyn during the development phase to catch issues early in the development lifecycle.
* **Custom Security Analysis**: By creating custom detectors, users can tailor the analysis to specific needs or concerns unique to their projects.
* **Competitive audit finding exclusion list**: Use Aderyn in your competitive audit platform to list findings as "known issues". This is the official tool run before [CodeHawks](https://www.codehawks.com/) competitions.

***

### Contributing

Aderyn is a fully open-source smart contract security and auditing tool powered by Cyfrin. It continually evolves, with future updates expected to streamline the installation process, enhance configuration options, and expand its analytical capabilities.

**Cyfrin loves open-source contributions.** **Please provide feedback or help us improve Aderyn by following the** [**Contribution Guidelines**](https://github.com/Cyfrin/aderyn/blob/dev/CONTRIBUTING.md) **on the official GitHub repo.**
