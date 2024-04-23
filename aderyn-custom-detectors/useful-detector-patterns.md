# Useful Detector Patterns

This page will find common patterns used when developing custom Aderyn detectors.

Check out the official Aderyn GitHub repository for more [examples of detectors and design patterns](https://github.com/Cyfrin/aderyn/tree/dev/aderyn\_core/src/detect).&#x20;

### Traversing the Abstract Syntax Tree (AST)

When writing a detector, a typical pattern is to find an [AST](what-is-an-ast.md) node (by getting it from the [`WorkspaceContext`](detectors-api-reference/workspacecontext.md) and then traverse the tree to its parent node or a child node for more information.

An example of traversing _up_ the tree to parent nodes is that you have a specific `VariableDeclaration`but want to know which `ContractDefinition` it is defined in. To do that, you must traverse _up_ the tree.

Conversely, suppose you have a `ContractDefinition` and want to find all the state variable `VariableDeclaration` nodes defined within it. In that case, you must traverse _down_ the tree from there `ContractDefinition` to its children.

Aderyn provides useful patterns for traversing _up_ and traversing _down_ the tree from any AST node.

#### Traversing _Down_

Patterns available to you:

1. `Extractor` Pattern - Get all descendents of a particular type from the current AST Node, regardless of depth.
2. `.children()` - Get the immediate children Nodes of the current AST Node/.

**1. `Extractor` Pattern**

From any ASTNode, you can extract all descendants of any particular Node type.

For example, to extract all `VariableDeclaration` nodes from a `ContractDefinition` node, the code would look like this:

```rust
let my_contract: &ContractDefinition = ...;
// Extract
let var_decs: Vec<VariableDeclaration> = ExtractVariableDeclarations::from(my_contract).extracted;
```

Note that this obtains _all_ `VariableDeclaration` nodes within that `ContractDefinition`, not just its immediate children. The full list of extractors is defined in [`extractor.rs`](https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/context/browser/extractor.rs).

**2. `.children()`**

From any ASTNode, get the immediate child nodes.

For example, take this Counter contract:&#x20;

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

contract Counter {
    uint256 public number;

    function setNumber(uint256 newNumber) public {
        number = newNumber;
    }

    function increment() public {
        number++;
    }
}
```

The immediate children of the `Counter` `ContractDefinition` is:

* `uint256 public number;` - `VariableDeclaration`
* `function setNumber(uint256 newNumber) public` - `FunctionDefinition`
* `function increment() public` - `FunctionDefinition`

So this code will return those children:

```rust
let contract_definition = ...;
let children = contract_definition.children(context);
```

#### Traversing _Up_&#x20;

Patterns available to you:

1. `.parent(WorkspaceContext)` - From the current AST Node, get its parent AST Node.
2. `.closest_ancestor_of_type(WorkspaceContext, NodeType)` - From the current node, traverse up the AST until you find an ancestor of a particular NodeType.
3. `.ancestral_line(WorkspaceContext)` - Get the entire ancestry chain from the current node to the `SourceUnit` node.

**1. `.parent(WorkspaceContext)`**

From any AST Node, get the immediate parent node. For example, from a `ContractDefinition` node, `.parent()` will return the `SourceUnit` parent.

```rust
let contract_definition = ...;
let parent = contract_definition.parent(context);
```

**2. `.closest_ancestor_of_type(WorkspaceContext, NodeType)`**

From an AST Node, traverse upwards until an ancestor of a particular NodeType is found.

For example, from a `FunctionDefinition`, find the `SourceUnit` ancestor.

```rust
let function_definition = ...;
let source_unit = function_definition.closest_ancestor_of_type(context, NodeType::SourceUnit);
```

**3. `.ancestral_line(WorkspaceContext)`**

From an AST Node, get the entire chain of ancestors up to the `SourceUnit`.

For example, from a `FunctionDefinition`, `.ancestral_line(context)` will return all ancestor nodes in an array, starting with the closest all the way to the `SourceUnit`.

```rust
let function_definition = ...;
let chain = function_definition.ancestral_line(context);
```
