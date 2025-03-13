# capture

### capture TBD

```rust
// Some code#[macro_export]
macro_rules! capture {
    ($self:ident, $context:ident, $item:expr) => {
        if let Some(id) = $context.get_node_id_of_capturable(&$item.clone().into()) {
            $self.found_instances.insert(
                $context.get_node_sort_key_from_capturable(&$item.clone().into()),
                id,
            );
        }
    };
}
```

**Definition:** [**https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/mod.rs#L8**](https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/mod.rs#L8)

**Usage:**

The `capture!` macro is designed to simplify the process of capturing instances of issues within the AST during analysis. It abstracts the boilerplate code necessary to check, capture, and store these instances based on their node IDs and sort keys.

Practically, it is responsible for populating the `found_instances` BTreeMap of the detector struct with the desired nodes. 

**Parameters:**

* `$self`: The self-reference of the issue detector instance.
* `$context`: The context in which the AST nodes are being analyzed, typically a reference to [`WorkspaceContext`](workspacecontext.md).
* `$item`: The item being captured as an issue instance, which could be a specific type of node like `Expression`, `Statement`, `ModifierDefinition`, etc. or even a more general `ASTNode`. 

#### Example

```rust
capture!(self, context, modifier);
```
