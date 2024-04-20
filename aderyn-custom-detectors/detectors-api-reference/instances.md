---
description: function used to detect vulnerabilities TBD
---

# instances

**`instances`**

```rust
fn instances(&self) -> BTreeMap<(String, usize, String), NodeID>
```

Definition: [https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/detector.rs#L195](https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/detector.rs#L195)

Maps the occurrences of the detected issue within the source code to their respective locations. This is primarily used by aderyn to print the report. (you don't need to worry about this function)

**Returns:**

* `BTreeMap<(String, usize, String), NodeID>`: A binary tree map where each key is a tuple containing:
  * `String`: The source file name where the issue is located.
  * `usize`: The line number of the issue.
  * `String`: A string representation of the source location (could be a character range or a more abstract descriptor).
  * `NodeID`: The node identifier in the AST corresponds to the issue.

```rust
fn name(&self) -> String {
        format!("{}", IssueDetectorNamePool::SolmateSafeTransferLib)
    }
```

