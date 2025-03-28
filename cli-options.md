---
description: Below are options which may be included with the aderyn CLI command.
---

# CLI Options

> If you are looking to leverage these options in VS Code extension, please use  aderyn.toml file instead, [https://cyfrin.gitbook.io/cyfrin-docs/aderyn-vs-code/aderyn.toml-configuration](https://cyfrin.gitbook.io/cyfrin-docs/aderyn-vs-code/aderyn.toml-configuration) That makes the configuration persistent for the project.&#x20;

```sh
aderyn [OPTIONS]
```

### **`aderyn <ROOT>`**

The root directory of your Solidity project.

**Input:**

`aderyn .`

***

### **`--help`**

Outputs the options and arguments available when using Aderyn.

{% code overflow="wrap" %}
```
Rust based Solidity AST analyzer

Usage: aderyn [OPTIONS] [ROOT] [COMMAND]

Commands:
  registry  Browse detector registry
  init      Initialize aderyn.toml in the root directory or in an optional subdirectory
  help      Print this message or the help of the given subcommand(s)

Arguments:
  [ROOT]
          Foundry or Hardhat project root directory (or path to single solidity file)

          [default: .]

Options:
  -s, --src <SRC>
          Path to the source contracts. Used to avoid analyzing libraries, tests or scripts and focus on the contracts.

          In Foundry projects, it's auto-captured by foundry.toml and it's usually not necessary to provide it.

          In a Hardhat project:

          --src=contracts/

  -i, --path-includes <PATH_INCLUDES>
          List of path strings to include, delimited by comma (no spaces).

          It allows to include only one or more specific contracts in the analysis: aderyn -i src/MyContract.sol aderyn -i src/MyContract.sol,src/MyOtherContract.sol

  -x, --path-excludes <PATH_EXCLUDES>
          List of path strings to exclude, delimited by comma (no spaces).

          It allows to exclude one or more specific contracts from the analysis: aderyn -x src/MyContract.sol aderyn -x src/MyContract.sol,src/MyOtherContract.sol

  -o, --output <OUTPUT>
          Desired file path for the final report (will overwrite existing one)

          [default: report.md]

  -l, --lsp
          [BETA] Start Aderyn's LSP server on stdout

      --no-snippets
          Do not include code snippets in the report (reduces report size in large repos)

      --highs-only
          Only use the high detectors

      --stdout
          Print the output to stdout instead of a file

      --skip-cloc
          Skip cloc analysis (line numbers, etc.)

      --skip-update-check
          Skip checking for new versions of Aderyn

      --auditor-mode
          Run in Auditor mode, which only outputs manual audit helpers

  -h, --help
          Print help (see a summary with '-h')

  -V, --version
          Print version

```
{% endcode %}

***

### **`-o, --output <OUTPUT>`**&#x20;

\- The default output is `report.md`. This can be renamed to anything you'd like. Currently supported formats include Markdown and JSON. JSON is particularly useful in CI/CD pipelines to compile properties from the generated report.

**Examples:**

```
aderyn -o my-report.json
```

```
aderyn -o my-report.md
```

***

### **`-s, --src <SOURCE_PATH>`**

The path to the source contracts folder. If not provided, the `ROOT` directory will be used.

If your project has a `foundry.toml` file in the ROOT, then aderyn will obtain this value from it.

**Examples based on the below directory structure:**

```
└── my_project/
    ├── hardhat.config.js
    ├── contracts/
    │   ├── Apples.sol
    │   └── Bananas.sol
    ├── script/
    │   └── Deploy.dol
    ├── test/
    │   ├── Apples.test.js
    │   └── Bananas.test.js
    ├── util/
    └── node_modules/
```

**Command:**

`aderyn --src contracts/`

***

### **`-i, --path-includes <PATH_INCLUDES>`**&#x20;

A string, or list of strings separated by commas that pertain to the filenames/directories in scope. These are the files/directories that Aderyn will be run on.

Note: strings passed to the scope command are case-sensitive.

**Examples will be based on the below repo:**

{% code fullWidth="false" %}
```
├── src
│   ├── interfaces
│   │   ├── IFlashLoanReceiver.sol
│   │   ├── IPoolFactory.sol
│   │   ├── ITSwapPool.sol
│   │   └── IThunderLoan.sol
│   ├── protocol
│   │   ├── AssetToken.sol
│   │   ├── OracleUpgradeable.sol
│   │   └── ThunderLoan.sol
│   └── upgradedProtocol
│       └── ThunderLoanUpgraded.sol
```
{% endcode %}

**Input:**

`aderyn -i src/interfaces`&#x20;

**Output:**

| Filepath                              | nSLOC  |
| ------------------------------------- | ------ |
| src/interfaces/IFlashLoanReceiver.sol | 13     |
| src/interfaces/IPoolFactory.sol       | 4      |
| src/interfaces/ITSwapPool.sol         | 4      |
| src/interfaces/IThunderLoan.sol       | 4      |
| **Total**                             | **25** |

**Input:**

`aderyn --path-includes Thund`

**Output:**

| Filepath                                     | nSLOC   |
| -------------------------------------------- | ------- |
| src/interfaces/IThunderLoan.sol              | 4       |
| src/protocol/ThunderLoan.sol                 | 176     |
| src/upgradedProtocol/ThunderLoanUpgraded.sol | 172     |
| **Total**                                    | **352** |

***

### **`-x, --path-excludes <PATH_EXCLUDE>`**&#x20;

the opposite of `--path-includes`, this will exclude any files or directories that contain the passed string.

**Input:**

`aderyn -x Thunder`

**Output:**

| Filepath                              | nSLOC   |
| ------------------------------------- | ------- |
| src/interfaces/IFlashLoanReceiver.sol | 13      |
| src/interfaces/IPoolFactory.sol       | 4       |
| src/interfaces/ITSwapPool.sol         | 4       |
| src/protocol/AssetToken.sol           | 65      |
| src/protocol/OracleUpgradeable.sol    | 23      |
| **Total**                             | **109** |

***

### **`-n, --no-snippets`**&#x20;

The default behavior is to include the line number, as well as snippets of code where the vulnerability is detected within the generated report.  This can potentially take up a lot of space in the report. This option will disable the snippets, leaving the line number readouts only.

**Input (default):**

`` aderyn -i Thunder` ``

*   Found in src/protocol/ThunderLoan.sol Line: 239

    ```solidity
        function setAllowedToken(IERC20 token, bool allowed) external onlyOwner returns (AssetToken) {
    ```

**Input (no-snippets):**

```
aderyn -i Thunder -n
aderyn -i Thunder --no-snippets
```

**Output:**

* Found in src/protocol/ThunderLoan.sol Line: 239

***

### **`aderyn --version`**&#x20;

Outputs the current version of Aderyn installed

**Input:**

```
aderyn -v
aderyn --version
```

**Output:**

`aderyn 0.0.13`

***

### `aderyn registry`

Output the list of detectors.

**Input:**

```
aderyn registry
```

**Output:**

```
Detector Registry

Name                             Title

Low

centralization-risk            - Centralization Risk for trusted owners
solmate-safe-transfer-lib      - Solmate's SafeTransferLib does not check for token contract's existence
avoid-abi-encode-packed        - `abi.encodePacked()` should not be used with dynamic types when passing the result to a hash function such as `keccak256()`
ecrecover                      - `ecrecover` is susceptible to signature malleability
...

High
...
```
