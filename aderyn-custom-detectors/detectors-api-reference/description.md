---
description: function used to detect vulnerabilities TBD
---

# description

**`description`**

```rust
fn description(&self) -> String
```

Definition: [https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/detector.rs#L195](https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/detector.rs#L195)

Gives a detailed description of the issue.

**Returns:**

* `String`: A string containing a detailed description of what the issue is, why it is significant, and possibly how to fix it.

#### Example

```rust
    fn description(&self) -> String {
        String::from("There is a subtle difference between the implementation of solmate's SafeTransferLib and OZ's SafeERC20: OZ's SafeERC20 checks if the token is a contract or not, solmate's SafeTransferLib does not.\nhttps://github.com/transmissions11/solmate/blob/main/src/utils/SafeTransferLib.sol#L9 \n`@dev Note that none of the functions in this library check that a token has code at all! That responsibility is delegated to the caller`\n")
    }

```



