# What is a Detector?

Adapting an **enterprise-level Solidity static analyzer** to your codebase can be daunting. Cyfrin Aderyn solves this by giving smart contract developers and security researchers an o**pen-source tool to easily write, test, run, and contribute** with their custom Aderyn static analysis detectors tailored to their needs.

Suppose you're unfamiliar with the concept of detectors: a detector is a snippet of code that, given a smart contract [Abstract Syntax Tree ](what-is-an-ast.md)(AST), will **verify the presence of vulnerabilities** based on user-defined patterns.&#x20;

If you've ever built a scraper, the concept is very similar.

***

### Aderyn static analysis detector

When you build a web scraper/crawler, you usually write a Python script that, given a URL, takes the content of a web page, filters it to find the exact information you need, and performs operations with that data based on your needs.

Let’s say you want to save the biographies of all Twitter users. You would feed a list of Twitter users' URLs into your script that should then filter through the HTML of the scraped page, find the text, and save those biographies - if the biography isn't there, continue.

**Detectors and Aderyn essentially work the same way:**

_Overly simplified:_ Aderyn is the scraping library, acting as the scraper; you give it a smart contract (a URL), and it will create a JSON-like representation of your smart contract or code base, called [AST](what-is-an-ast.md) or [Abstract Syntax Tree](what-is-an-ast.md), just like the content of your HTML page, it will contain all the data you need about your smart contract's code.

Let's say that you have the following code:

```solidity
//SPDX-License-Identifier: UNLICENSED
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

The AST of the code above will look as follows:

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

Source: [https://astexplorer.net/#/gist/1bf9b4c8449ef55de8057cb47334daf0/3ef42aad949250d3b492c51b67f3739fe2fc5f3d](https://astexplorer.net/#/gist/1bf9b4c8449ef55de8057cb47334daf0/3ef42aad949250d3b492c51b67f3739fe2fc5f3d)

As you can see, the AST contains information like:

* **contract name**
* **function names**
* **definitions**
* **variables**
* **modifiers**

Essentially, **all the relevant information about your Solidity smart contract** code and its content. You can [read more about AST](what-is-an-ast.md) on the dedicated documentation page.

While Aderyn provides you with the AST, the detectors running on it verify that the data inside the AST contains the right things at the right place, and if not, it means there's a vulnerability.

Let's make an example.

***

### **Example of an Aderyn Detector**

Let's say we must ensure that the **nonReentrant modifier is the first assigned to each appropriate function** in my codebase.

That means every function should be:

```jsx
     function setOwner(address _owner) external nonReentrant onlyOwner {
```

and not:

```jsx
     function setOwner(address _owner) external onlyOwner nonReentrant {
```

If the nonReentrant modifier isn’t the first assigned, we might incur **reentrancy issues** inside other modifiers.&#x20;

With the information in our code's Abstract Syntax Tree  (AST), we can [build a detector](detectors-quickstart.md) that checks through all the modifiers assigned to every function in the codebase and verifies that "nonReentrant" is the first one assigned. If not, it should be reported.

Here's how the detector would look like:

```rust
pub struct NonReentrantBeforeOthersDetector {
    // Keys are source file name and line number
    found_instances: BTreeMap<(String, usize, String), NodeID>,
}

impl IssueDetector for NonReentrantBeforeOthersDetector {
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
  }
```

Source: [https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/nc/non\_reentrant\_before\_others.rs](https://github.com/Cyfrin/aderyn/blob/dev/aderyn\_core/src/detect/nc/non\_reentrant\_before\_others.rs)

In the code above, we’re declaring a new detector called, to which we attach an IssueDetector that implements the [detect()](detectors-api-reference/detect.md) function.

Inside the [detect](detectors-api-reference/detect.md)[()](detectors-api-reference/detect.md) function, we can use the **AST representation of our smart contract** to run the logic to find if the modifier is the first assigned to every function.

To do it, we:

* Loop through each function definition
* For each function, the modifiers array length
* If the length is >1
* Check if there is a `nonReentrant` modifier
* If there is, and is not at position zero - YOU FOUND AN ISSUE!

As simple as that. Like filtering through our HTML tags, we can traverse the AST representation of our solidity smart contract and write code that finds vulnerabilities while you write them.

Now that you know what a detector is and what it looks like, learn how to [write your custom detector ](detectors-quickstart.md)or find more examples of custom detectors on the [official Aderyn playground GitHub repo](https://github.com/Cyfrin/aderyn-contracts-playground).

### **Where do I find vulnerability patterns?**

Get access to **8000+ smart contract findings**, **vulnerabilities**, bug bounties, and competitions completely free on [Cyfrin Solodit](https://solodit.xyz).

Learn from the world’s top auditors and create detectors to spot those vulnerabilities while you can, using Cyfrin Aderyn.

***

### Conclusion

A detector is a snippet of code that, given a smart contract Abstract Syntax Tree (AST), will verify the presence of vulnerabilities based on user-defined patterns.

Developers can [study vulnerability patterns on Solodit](https://solodit.xyz) and develop their custom detectors, tailored to their codebase, using Cyfrin Aderyn.
