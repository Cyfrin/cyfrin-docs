# What is Aderyn CI Assistant ?

{% hint style="warning" %}
**Aderyn CI Assistant is retired and is no longer maintained.** Its GitHub Marketplace listing has been removed. Read the [retirement notice and migration guidance](https://aderyn.cyfrin.io/retirement).
{% endhint %}

Aderyn CI Assistant was a GitHub Action that ran static analysis on Solidity codebases in CI. Its source and historical references remain available for reference.

### Existing workflows

Marketplace removal does not remove workflow steps referencing an action tag or commit SHA. Remove or replace steps using `Cyfrin/aderyn-ci` in maintained workflows, and update any jobs or branch rules that depend on those checks. Workflows that download withdrawn Aderyn binaries may fail.

### Historical configuration example

The example below is retained to help identify existing references. Do not add it to new workflows.

```yaml
- name: Aderyn Check
  uses: Cyfrin/aderyn-ci@v0
  with:
    fail-on: high
```

