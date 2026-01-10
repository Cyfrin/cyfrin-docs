# Testing your detector

Testing is key, not only when writing smart contracts but also when writing the detectors to test them.&#x20;

Testing an Aderyn detector is extremely easy, as it's built in Rust and can be tested as any other Rust code, with the only difference being that you will need a Solidity smart contract implementing the vulnerability your detector has to find.&#x20;

Luckily, Cyfrin Aderyn has a series of smart contracts in the `tests/contracts_playground/src` folder, which you can use to test your detectors.

You can also find the same contracts in the [standalone contracts-playground repository](https://github.com/cyfrin/aderyn-contracts-playground/).

Now, let's say we want to test the detector we've built in the [Detectors quickstart guide](./), whose only job is ensuring that all **modifiers assigned to every function are used** and that there are no useless modifiers.&#x20;

Simplified, the detector looks like this:

```rust
pub struct MyFirstDetector {
    // Keys are source file name and line number
    found_instances: BTreeMap<(String, usize, String), NodeID>,
}

impl IssueDetector for MyFirstDetector {
    fn detect(&mut self, context: &WorkspaceContext) -> Result<bool, Box<dyn Error>> {
        for modifier in context.modifier_definitions() {
            let mut count = 0;
            for inv in context.modifier_invocations() {
                if let Some(id) = inv.modifier_name.referenced_declaration {
                    if id == modifier.id {
                        count += 1;
                    }
                }
            }
            if count == 1 {
                capture!(self, context, modifier);
            }
        }

        Ok(!self.found_instances.is_empty())
    }
}
```

To test it, we will use the [OnceModifierExample.sol](https://github.com/Cyfrin/aderyn/blob/dev/tests/contract-playground/src/OnceModifierExample.sol) contract available in the `tests/contracts_playground/contracts_playground` folder:&#x20;

```solidity
SPDX-License-Identifier: MIT
pragma solidity 0.8.19;

contract OnceModifierExample {
 
    modifier onlyOnce() {
        _;
    }

    function perform() external onlyOnce {
        
    }
}
```

As you can notice, the `perform()` function has the `onlyeOnce` modifier assigned only, which does nothing, our detector should find it and report it - to test this is true, let's copy-paste the following code under our detector declaration:

```rust
#[cfg(test)]
mod useless_modifier_tests {
    use crate::detect::detector::{detector_test_helpers::load_contract, IssueDetector};

    use super::UselessModifierDetector;

    #[test]
    fn test_useless_modifier_tests() {
        let context = load_contract(
            "../tests/contract-playground/out/OnceModifierExample.sol/OnceModifierExample.json",
        );

        let mut detector = UselessModifierDetector::default();
        // assert that the detector finds the public Function
        let found = detector.detect(&context).unwrap();
        assert!(found);
        // assert that the detector returns the correct number of instances
        assert_eq!(detector.instances().len(), 1);
        // assert that the detector returns the correct severity
        assert_eq!(
            detector.severity(),
            crate::detect::detector::IssueSeverity::Low
        );
        // assert that the detector returns the correct title
        assert_eq!(
            detector.title(),
            String::from("Modifiers invoked only once can be shoe-horned into the function")
        );
        // assert that the detector returns the correct description
        assert_eq!(detector.description(), String::from(""));
    }
}
```

In the code above, we are:

* Importing the [OnceModifierExample.sol](https://github.com/Cyfrin/aderyn/blob/dev/tests/contract-playground/src/OnceModifierExample.sol) smart contract AST
* Run the detect function
* Assert if we've effectively found the vulnerability

To run the one test we just made, run the following command in your terminal:

```bash
cargo test test_useless_modifier_tests
```

Or, to run all the tests:

```bash
cargo test 
```

If the vulnerability was found, the detector successfully worked, and you're ready to use it, publish it, and contribute to Aderyn. TODO

You can learn more about [creating tests on Rusts](https://doc.rust-lang.org/book/ch11-01-writing-tests.html) using the official documentation.
