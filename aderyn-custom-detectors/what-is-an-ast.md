# What is an AST?

An AST, or **Abstract Syntax Tree**, is a structured representation of code primarily compilers use to read code and generate the target binaries. It is often stored as JSON.

Let's take the following code as an example:

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

Think of this contract like "levels" of syntax. If we take its code and compile it, we'll obtain something similar to the simplified AST representation of the Counter.sol example, shown above:

```json
{
  "type": "SourceUnit",
  "children": [ 
    {
      "type": "PragmaDirective",
      ...
    },
    {
      "type": "ContractDefinition",
      "name": "Counter",
      "subNodes": [
        {
          "type": "StateVariableDeclaration",
          "variables": [
            {
              "type": "VariableDeclaration",
              "name": "number",
              ...
            }
          ],
          ...
        },
        {
          "type": "FunctionDefinition",
          "name": "setNumber",
          "body": {
            ... // Deeper nodes that describe the function body
          },
          ...
        },
        {
          "type": "FunctionDefinition",
          "name": "increment",
          "body": {
            ... // Deeper nodes that describe the function body
          },
          ...
        }
      ],
      ...
    }
  ],
  ...
}
```

Source: [Counter contract on ASTExplorer.net](https://astexplorer.net/#/gist/1bf9b4c8449ef55de8057cb47334daf0/3ef42aad949250d3b492c51b67f3739fe2fc5f3d)

_"..." refers to information hidden for this structural example._

#### Level 0 - `SourceUnit`

At the _base_ level (file level), what can we define in Solidity?

* License
* Pragma
* Contract Definitions
* Event Definitions
* etc

This base level is known as the `SourceUnit` in AST terminology. Imagine this `SourceUnit` as a node in a tree. In our example, our `SourceUnit` has 3 children:

1. License -  `// SPDX-License-Identifier: UNLICENSED`&#x20;
2. Pragma - `pragma solidity ^0.8.13;`
3. Contract Definition - `contract Counter`

In AST, each one of these, including the `SourceUnit` are referred to as "Nodes" or "AST Nodes".

#### Level 1 - `ContractDefinition`

Let's go one level deeper and into the  `counter` Contract Definition. It has its requirements regarding what possible children it can have. For example, inside the Contract Definition, the Solidity compiler will accept:

* Function Definitions
* Modifier Definitions
* Constructors
* State Variables
* Constants
* etc

In our example, the `counter`contract has 3 direct children:

1. Variable Declaration - `uint256 public number;`
2. Function Definition - `function setNumber(uint256 newNumber) public`
3. Function Definition - `function increment() public`

The whole structure can be represented as a tree, where the top node is a `SourceUnit`.

Each level has information about every single Node in the tree and everything in the source code.

## Explore more about AST.

To see a more detailed version of the AST,[ see this Counter contract on ASTExplorer.net](https://astexplorer.net/#/gist/1bf9b4c8449ef55de8057cb47334daf0/3ef42aad949250d3b492c51b67f3739fe2fc5f3d) and poke around!
