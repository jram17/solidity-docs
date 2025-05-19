# 5. Control structures and Error handling
Smart contracts must make decisions, iterate over data, and handle unexpected situations gracefully. Solidity offers a familiar set of control structures along with specialized tools for error handling and function-level access control.

This module covers Solidity’s core logic tools: **conditionals**, **loops**, **error handling**, and **modifiers.**all of which are critical to writing robust and secure contracts.

## Conditionals and Loops

### Conditionals

Used to make decisions based on boolean expressions.

```jsx
if (balance > 0) {
    // logic
} else {
    // alternative logic
}

```

### Loops

Used for iteration. Solidity provides `for`, `while`, and `do-while` loops.

```jsx
// for loop example
for (uint i = 0; i < users.length; i++) {
    process(users[i]);
}

// while loop example
while (i < limit) {
    i++;
}

// Loops can be expensive in gas. Avoid unbounded loops in smart contracts.

```

## Error Handling

Solidity provides three primary mechanisms for detecting and handling errors: `require`, `revert`, and `assert`.

**require( condition , message )**

-   Validates **inputs and external conditions**.
-   Reverts the transaction **with a message** if the condition is false.

```jsx
require(balance >= amount, "Insufficient balance");

```

**revert( message )**

-   Used to **explicitly revert** a transaction, often after complex logic.
-   More flexible than `require`, especially in nested conditions.

```jsx
if (userBlocked) {
    revert("User is blocked");
}

```

**assert( condition )**

-   Used for **internal errors and invariants** that should never fail.
-   Consumes all remaining gas on failure.

```jsx
assert(totalSupply <= MAX_SUPPLY);

```

> Prefer require for user input checks, revert for logic-based aborts, and assert for critical internal validations.

### Custom Error Definitions (Solidity 0.8+)

Custom errors are a gas-efficient alternative to revert strings. They allow for clearer and more structured error reporting.

```jsx
error Unauthorized(address caller);

function restrictedAction() public {
    if (msg.sender != owner) {
        revert Unauthorized(msg.sender);
    }
}

// Custom errors save gas by avoiding long revert strings and provide typed error handling.

```

## Modifier Functions

Modifiers are reusable code blocks that run **before** (and optionally after) a function executes. They're commonly used for access control, validations, or pausing logic.

```jsx
modifier onlyOwner() {
    require(msg.sender == owner, "Not the owner");
    _;
}

function withdraw() public onlyOwner {
    // owner-only logic
}

```

