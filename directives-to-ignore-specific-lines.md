# Aderyn - Ignore specific lines

Static analyzers, including Aderyn, may sometimes report issues that are false positives or that you intentionally choose not to address. Aderyn provides multiple ways to acknowledge these issues and skip their detection for specific lines.

**Example**

Consider the following code:

```solidity
// aderyn-ignore-next-line(centralization-risk, state-change-without-event)  
function withdraw() external onlyOwner {  
    uint256 l = s_funders.length;  

    // aderyn-ignore-next-line(costly-loop)  
    for (uint256 funderIndex = 0; funderIndex < l; funderIndex++) {  
        address funder = s_funders[funderIndex];  
        delete s_addressToAmountFunded[funder];  
    }  
    ...  
}  
```



In this snippet, Aderyn flags the `withdraw()` function for **centralization risk** and **state change without an event**. If you, as the developer, are aware of these risks and accept them, you can suppress these warnings using one of the following methods:



**Ignore the next line**

Place the directive above the problematic line

```
// aderyn-ignore-next-line(detector-name)
```



**Ignore the current line**

Place the directive on the same line:

```
// aderyn-ignore(detector-name)  
```



**Ignoring All Detectors**

If you want Aderyn to skip a line entirely, regardless of the detector, you can use:

```
// aderyn-ignore  
```

```
// aderyn-ignore-next-line  
```

Note that in this case, you **do not** need to specify the detector name in parentheses.





> NOTE
>
> We're curerntly working on making a semantic separation between directives that are meant to ignore legitimiate issues vs **false positives**.
>
> That would look something like `//aderyn-fp(detector-name)` It would behave exactly the same way as the above ignore directives.&#x20;



