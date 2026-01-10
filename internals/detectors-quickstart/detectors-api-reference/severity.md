---
description: function used to detect vulnerabilities TBD
---

# severity

**`severity`**

```rust
fn severity(&self) -> IssueSeverity
```

Definition: [https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/detector.rs#L195](https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/detector.rs#L195)

Returns the severity level of the issue detected by the implementor of this trait.

**Returns:**

* `IssueSeverity`: The severity of the issue, which could be `Low`, `Medium`, or `High`.

#### Example

```rust
fn severity(&self) -> IssueSeverity {
        IssueSeverity::High
    }
```

#### Issue Severity Enum

```rust
pub enum IssueSeverity {
    Low,
    High,
}
```

source: [https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/detector.rs#L186](https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/detector.rs#L186)

