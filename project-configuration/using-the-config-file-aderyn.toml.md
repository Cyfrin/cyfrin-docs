# Using the config file - aderyn.toml

Aderyn works seamlessly on commonly recognized project structures, i.e., when a `foundry.toml` or `hardhat.config.js` is found in the workspace's root. By default all detectors are run and all files in the project source are included.&#x20;

### Initialization

**To customize this behavior of Aderyn, initialize  `aderyn.toml`  config file in the project root by doing either of the following :**\
\
1\.  Run `aderyn init`  when using command line version of Aderyn\
\
2\. Pick the action `Aderyn: Initialize Config File`  in VS Code command palette   by pressing <kbd>Ctrl/Cmd + Shift + P</kbd>  when using the VS Code extension&#x20;

***

#### Guide to understand customization keys

### Version

```toml
version = 1
```

* **Description**: Specifies the version of the configuration file format.
* **Note**: As of now, only version `1` is supported. Do not change this value.

***

### Root

```toml
root = "."
```

* **Description**: Defines the base path for resolving remappings and compiling smart contracts. This path is relative to the workspace root (the directory where the editor is open).
* **Default**: `.` (current directory).
* **Recommendation**: Typically, this should point to the directory containing `foundry.toml` or `hardhat.config.js/ts`.

***

### Source Directory (`src`)

```toml
src = "src/"
```

* **Description**: Specifies the path to the directory containing your smart contracts, relative to the `root` directory. Aderyn will traverse all nested files within this directory to scan for vulnerabilities.
* **Default**: If not specified, Aderyn will attempt to extract this value from the framework being used (e.g., Foundry or Hardhat).
  * For **Hardhat**, the default is `contracts/`.
  * For **Foundry**, the default depends on `foundry.toml` and other factors like the `FOUNDRY_PROFILE` environment variable.
* **Override**: If specified, Aderyn will use this value instead of the framework-derived path.

***

### Include Files (`include`)

```toml
include = ["src/counters/Counter.sol", "src/others/"]
include = ["/interfaces/"]
```

* **Description**: Specifies the path segments of contract files to include in the analysis.
* **Behavior**:
  * You can use partial matches (e.g., `/interfaces/`) to include all files containing that segment in their path.
  * You can use full matches (e.g., `src/counters/Counter.sol`) to include only the exact file.
* **Default**: If not specified, all contract files in the source directory will be included.

***

### Exclude Files (`exclude`)

```toml
exclude = ["src/counters/Counter.sol", "src/others/"]
exclude = ["/interfaces/"]
```

* **Description**: Specifies the path segments of contract files to exclude from the analysis.
* **Behavior**:
  * You can use partial matches (e.g., `/interfaces/`) to exclude all files containing that segment in their path.
  * You can use full matches (e.g., `src/counters/Counter.sol`) to exclude only the exact file.
* **Default**: If not specified, no contract files will be excluded.

***

### Remappings

* **Description**: Aderyn uses remappings to resolve dependencies in your project.
* **Behavior**:
  * Remappings can be specified in a `remappings.txt` file within the root folder of the project.
  * If not specified, Aderyn will attempt to derive remappings from `foundry.toml` (if present).

***

### Environment Variables (`env`)

```toml
[env]
FOUNDRY_PROFILE = "default"
```

* **Description**: Specifies environment variables that Aderyn should use during analysis.
* **Use Case**: Useful for advanced configurations, such as when different profiles in `foundry.toml` have different `src` declarations. For example, setting `FOUNDRY_PROFILE` can dictate the correct `src` value.
* **Default**: If not specified, Aderyn will use the system's environment variables.

***

### Include Or Exclude Detectors

**Description**: To include or exclude to specific detectors, find out the names of the detectors either by hovering over the underlined issue if you are using the VS Code extension or by simply running `aderyn registry` if you are using Command Line version of Aderyn.<br>

**Default**: All detectors are run.\
\
**Behavior**:\
Use the following syntax to include or exclude specific detectors\
\
Examples

```
[detectors]
include = ["unspecific-solidity-pragma", "unused-state-variable"]
```

```
[detectors]
exclude = ["unspecific-solidity-pragma", "unused-state-variable"]
```

***

### Example Configuration

Here’s an example of a complete `aderyn.toml` file:

```toml
version = 1

root = "."

include = ["src/counters/Counter.sol", "/interfaces/"]
exclude = ["src/others/", "/test/"]

[env]
FOUNDRY_PROFILE = "ccip"
```

***
