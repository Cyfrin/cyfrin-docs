# WorkspaceContext

The `WorkspaceContext` struct is designed to manage and interact with an Abstract Syntax Tree (AST) of source code. It facilitates access to various node types in the AST and provides methods to retrieve parental and ancestral relationships between these nodes. The following API documentation details the methods implemented in the `WorkspaceContext` struct.

Definition: [https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/context/workspace\_context.rs](https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/context/workspace\_context.rs)

### WorkspaceContext Struct API Reference - Getters

The getters in the `WorkspaceContext` struct provides access to vectors of references to various AST node types, each stored in a separate context within the struct. These methods are crucial for retrieving collections of specific node types for analysis or manipulation.

#### Getters

**`array_type_names`**

```rust
pub fn array_type_names(&self) -> Vec<&ArrayTypeName>
```

Retrieves all `ArrayTypeName` nodes from the AST.

**Returns:**

* `Vec<&ArrayTypeName>`: A vector of references to `ArrayTypeName` nodes.

**`assignments`**

```rust
pub fn assignments(&self) -> Vec<&Assignment>
```

Retrieves all `Assignment` nodes from the AST.

**Returns:**

* `Vec<&Assignment>`: A vector of references to `Assignment` nodes.

**`binary_operations`**

```rust
pub fn binary_operations(&self) -> Vec<&BinaryOperation>
```

Retrieves all `BinaryOperation` nodes from the AST.

**Returns:**

* `Vec<&BinaryOperation>`: A vector of references to `BinaryOperation` nodes.

**`blocks`**

```rust
pub fn blocks(&self) -> Vec<&Block>
```

Retrieves all `Block` nodes from the AST.

**Returns:**

* `Vec<&Block>`: A vector of references to `Block` nodes.

**`conditionals`**

```rust
pub fn conditionals(&self) -> Vec<&Conditional>
```

Retrieves all `Conditional` nodes from the AST.

**Returns:**

* `Vec<&Conditional>`: A vector of references to `Conditional` nodes.

**`contract_definitions`**

```rust
pub fn contract_definitions(&self) -> Vec<&ContractDefinition>
```

Retrieves all `ContractDefinition` nodes from the AST.

**Returns:**

* `Vec<&ContractDefinition>`: A vector of references to `ContractDefinition` nodes.

**`elementary_type_names`**

```rust
pub fn elementary_type_names(&self) -> Vec<&ElementaryTypeName>
```

Retrieves all `ElementaryTypeName` nodes from the AST.

**Returns:**

* `Vec<&ElementaryTypeName>`: A vector of references to `ElementaryTypeName` nodes.

**`elementary_type_name_expressions`**

```rust
pub fn elementary_type_name_expressions(&self) -> Vec<&ElementaryTypeNameExpression>
```

Retrieves all `ElementaryTypeNameExpression` nodes from the AST.

**Returns:**

* `Vec<&ElementaryTypeNameExpression>`: A vector of references to `ElementaryTypeNameExpression` nodes.

**`emit_statements`**

```rust
pub fn emit_statements(&self) -> Vec<&EmitStatement>
```

Retrieves all `EmitStatement` nodes from the AST.

**Returns:**

* `Vec<&EmitStatement>`: A vector of references to `EmitStatement` nodes.

**`enum_definitions`**

```rust
pub fn enum_definitions(&self) -> Vec<&EnumDefinition>
```

Retrieves all `EnumDefinition` nodes from the AST.

**Returns:**

* `Vec<&EnumDefinition>`: A vector of references to `EnumDefinition` nodes.

**`enum_values`**

```rust
pub fn enum_values(&self) -> Vec<&EnumValue>
```

Retrieves all `EnumValue` nodes from the AST.

**Returns:**

* `Vec<&EnumValue>`: A vector of references to `EnumValue` nodes.

**`event_definitions`**

```rust
pub fn event_definitions(&self) -> Vec<&EventDefinition>
```

Retrieves all `EventDefinition` nodes from the AST.

**Returns:**

* `Vec<&EventDefinition>`: A vector of references to `EventDefinition` nodes.

**`error_definitions`**

```rust
pub fn error_definitions(&self) -> Vec<&ErrorDefinition>
```

Retrieves all `ErrorDefinition` nodes from the AST.

**Returns:**

* `Vec<&ErrorDefinition>`: A vector of references to `ErrorDefinition` nodes.

**`expression_statements`**

```rust
pub fn expression_statements(&self) -> Vec<&ExpressionStatement>
```

Retrieves all `ExpressionStatement` nodes from the AST.

**Returns:**

* `Vec<&ExpressionStatement>`: A vector of references to `ExpressionStatement` nodes.

**`function_calls`**

```rust
pub fn function_calls(&self) -> Vec<&FunctionCall>
```

Retrieves all `FunctionCall` nodes from the AST.

**Returns:**

* `Vec<&FunctionCall>`: A vector of references to `FunctionCall` nodes.

**`function_call_options`**

```rust
pub fn function_call_options(&self) -> Vec<&FunctionCallOptions>
```

Retrieves all `FunctionCallOptions` nodes from the AST.

**Returns:**

* `Vec<&FunctionCallOptions>`: A vector of references to \`FunctionCall

Options\` nodes.

**`function_definitions`**

```rust
pub fn function_definitions(&self) -> Vec<&FunctionDefinition>
```

Retrieves all `FunctionDefinition` nodes from the AST.

**Returns:**

* `Vec<&FunctionDefinition>`: A vector of references to `FunctionDefinition` nodes.

**`function_type_names`**

```rust
pub fn function_type_names(&self) -> Vec<&FunctionTypeName>
```

Retrieves all `FunctionTypeName` nodes from the AST.

**Returns:**

* `Vec<&FunctionTypeName>`: A vector of references to `FunctionTypeName` nodes.

**`for_statements`**

```rust
pub fn for_statements(&self) -> Vec<&ForStatement>
```

Retrieves all `ForStatement` nodes from the AST.

**Returns:**

* `Vec<&ForStatement>`: A vector of references to `ForStatement` nodes.

**`identifiers`**

```rust
pub fn identifiers(&self) -> Vec<&Identifier>
```

Retrieves all `Identifier` nodes from the AST.

**Returns:**

* `Vec<&Identifier>`: A vector of references to `Identifier` nodes.

**`identifier_paths`**

```rust
pub fn identifier_paths(&self) -> Vec<&IdentifierPath>
```

Retrieves all `IdentifierPath` nodes from the AST.

**Returns:**

* `Vec<&IdentifierPath>`: A vector of references to `IdentifierPath` nodes.

**`if_statements`**

```rust
pub fn if_statements(&self) -> Vec<&IfStatement>
```

Retrieves all `IfStatement` nodes from the AST.

**Returns:**

* `Vec<&IfStatement>`: A vector of references to `IfStatement` nodes.

_\[Methods continue in a similar format for_ [_each specific AST node type_](https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/context/workspace\_context.rs#L1047)_]_

### Navigation Methods

Methods in this section are used to navigate the AST based on node relationships.

**`get_parent`**

```rust
pub fn get_parent(&self, node_id: NodeID) -> Option<&ASTNode>
```

Fetches the parent node of the specified node ID.

**Parameters:**

* `node_id`: The unique identifier for an AST node, typically encapsulating the location or the specific instance of the node within the AST.

**Returns:**

* `Option<&ASTNode>`: An optional reference to the AST node that is the parent of the specified node. Returns `None` if the parent does not exist.

**`get_ancestral_line`**

```rust
pub fn get_ancestral_line(&self, node_id: NodeID) -> Vec<&ASTNode>
```

Constructs the ancestral line of AST nodes from the specified node up to the root.

**Parameters:**

* `node_id`: The unique identifier for an AST node.

**Returns:**

* `Vec<&ASTNode>`: A vector containing references to each node in the ancestral line, starting from the specified node and extending to the root node.

**`get_closest_ancestor`**

```rust
pub fn get_closest_ancestor(&self, node_id: NodeID, node_type: NodeType) -> Option<&ASTNode>
```

Searches for the closest ancestor of the specified node that matches the given node type.

**Parameters:**

* `node_id`: The unique identifier for an AST node.
* `node_type`: The type of node to find as an ancestor (e.g., `FunctionDefinition`, `Block`).

**Returns:**

* `Option<&ASTNode>`: An optional reference to the closest ancestor node of the specified type. Returns `None` if no such ancestor exists.
