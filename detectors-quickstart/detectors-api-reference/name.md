---
description: function used to detect vulnerabilities TBD
---

# name

**`name`**

```rust
fn name(&self) -> String
```

Definition: [https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/detector.rs#L195](https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/detector.rs#L195)

Returns the name of the detector as specified in `IssueDetectorNamePool`, which categorizes the type of issue.

**Returns:**

* `String`: A string representation of the issue detector's name, helpful for identifying and categorizing different types of detectors.



#### Example

```rust
fn name(&self) -> String {
        format!("{}", IssueDetectorNamePool::ArbitraryTransferFrom)
}
```

Definition

###
