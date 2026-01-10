# What is Aderyn CI Assistant ?

Aderyn CI Assistant is a Github Action that  performs static analysis on Solidity codebases in Github CI to catch potential vulnerabilities before committing code. \
\
Available for free, check it out on the [marketplace](https://github.com/marketplace/actions/aderyn-ci-assistant).<br>

#### Quick Start

```
- name: Aderyn Check
  uses: Cyfrin/aderyn-ci@v0
  with:
    fail-on: high
```

