# aderyn.toml Configuration

> _**If your project uses Foundry or Hardhat, Aderyn will automatically inherit the configuration from your foundry.toml or hardhat.config file.**_

To run Aderyn on a project that does not use a well-known framework like Foundry or Hardhat, configure `aderyn.toml`   for predictable detection. Aderyn may work without configuring this file, but it is strongly recommended that you do.

To instantiate the config file for customization purposes, either run `aderyn init`  or if you are using the VS Code extension, run the following command after pressing <kbd>Ctrl/Cmd + Shift + P</kbd>&#x20;

```
Aderyn: Initialize Config File
```

***

### **Version**

```toml
version = 1
```

* **Description**: Specifies the version of the configuration file format.
* **Note**: As of now, only version `1` is supported. Do not change this value.

***

### **Root**

```toml
root = "."
```

* **Description**: Defines the base path for resolving remappings and compiling smart contracts. This path is relative to the workspace root (the directory where the editor is open).
* **Default**: `.` (current directory).
* **Recommendation**: Typically, this should point to the directory containing `foundry.toml` or `hardhat.config.js/ts`.

***

### **Source Directory (`src`)**

```toml
src = "src/"
```

* **Description**: Specifies the path to the directory containing your smart contracts, relative to the `root` directory. Aderyn will traverse all nested files within this directory to scan for vulnerabilities.
* **Default**: If not specified, Aderyn will attempt to extract this value from the framework being used (e.g., Foundry or Hardhat).
  * For **Hardhat**, the default is `contracts/`.
  * For **Foundry**, the default depends on `foundry.toml` and other factors like the `FOUNDRY_PROFILE` environment variable.
* **Override**: If specified, Aderyn will use this value instead of the framework-derived path.

***

### **Include Files (`include`)**

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

### **Exclude Files (`exclude`)**

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

### **Remappings**

* **Description**: Aderyn uses remappings to resolve dependencies in your project.
* **Behavior**:
  * Remappings can be specified in a `remappings.txt` file within the root folder of the project.
  * If not specified, Aderyn will attempt to derive remappings from `foundry.toml` (if present).

***

### **Environment Variables (`env`)**

```toml
[env]
FOUNDRY_PROFILE = "default"
```

* **Description**: Specifies environment variables that Aderyn should use during analysis.
* **Use Case**: Useful for advanced configurations, such as when different profiles in `foundry.toml` have different `src` declarations. For example, setting `FOUNDRY_PROFILE` can dictate the correct `src` value.
* **Default**: If not specified, Aderyn will use the system's environment variables.

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
