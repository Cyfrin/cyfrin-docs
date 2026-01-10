---
description: function used to detect vulnerabilities TBD
---

# detect

**`detect`**

```rust
fn detect(&mut self, _context: &WorkspaceContext) -> Result<bool, Box<dyn Error>>
```

Definition:&#x20;

[https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/detector.rs#L195](https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/detector.rs#L195)

Evaluate the AST provided `WorkspaceContext` to determine if a particular code issue is present.

**Parameters:**

* `_context`: A reference to the [`WorkspaceContext`](workspacecontext.md) containing the AST nodes to be analyzed.

**Returns:**

* `Result<bool, Box<dyn Error>>`:
  * `Ok(true)` if an issue is detected; otherwise `Ok(false)`.
  * `Err(Box<dyn Error>)` if an error occurs during issue detection.

Example:

```rust
 fn detect(&mut self, context: &WorkspaceContext) -> Result<bool, Box<dyn Error>> {
        let function_definitions = context.function_definitions();
        for definition in function_definitions {
            if definition.modifiers.len() > 1 {
                for (index, modifier) in definition.modifiers.iter().enumerate() {
                    if modifier.modifier_name.name == "nonReentrant" && index != 0 {
                        capture!(self, context, modifier);
                    }
                }
            }
        }
        Ok(!self.found_instances.is_empty())
    }
```
