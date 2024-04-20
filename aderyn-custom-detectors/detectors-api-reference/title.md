---
description: Set the title of the vulnerability in the report TBD
---

# title

**`title`**

```rust
fn title(&self) -> String
```

Definition:  [https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/detector.rs#L195](https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/detector.rs#L195)

Provides a brief title or headline for the issue that the detector identifies.

**Returns:**

* `String`: A string representing the title of the issue.

#### Example:

```rust
fn title(&self) -> String {
        String::from("Your-finding-title")
    }
```





