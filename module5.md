# 5. Control structures and Error handling
> Master Pokémon Logic — Make Decisions, Avoid Critical Hits!

Your Pokémon knows its stats. It knows how to battle. But now it needs to make decisions in real time—should it use Thunderbolt or heal? Should it attack, retreat, or evolve? That’s where control flow comes in.

Just like any good Trainer, your smart contract Pokémon must handle the unexpected: wild variables, edge cases, and logic errors. Solidity gives you the tools to build smart Pokémon that think, react, and protect themselves from bugs and bad actors.


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

## Error Handling - When Moves Fail
> A good Trainer always checks if a move is legal before using it. Maybe your Pokémon doesn't have enough HP, or the trainer isn’t authorized

Solidity provides three primary mechanisms for detecting and handling errors: `require`, `revert`, and `assert`.

**require( condition , message )**

-   Validates **inputs and external conditions**.
-   Reverts the transaction **with a message** if the condition is false.

```jsx
require(hp > 0, "Fainted Pokémon can't fight!");
require(msg.sender == trainer, "Not your Pokémon!");


```

**revert( message )**

-   Used to **explicitly revert** a transaction, often after complex logic.
-   More flexible than `require`, especially in nested conditions.

```jsx
if (isConfused && random() < 50) {
    revert("Pokémon hurt itself in confusion!");
}

```

**assert( condition )**

-   Used for **internal errors and invariants** that should never fail.
-   Consumes all remaining gas on failure.

```jsx
assert(totalCaught <= MAX_POKEMON);

```

> Prefer require for user input checks, revert for logic-based aborts, and assert for critical internal validations.

### Custom Error Definitions (Solidity 0.8+)

Custom errors are a gas-efficient alternative to revert strings. They allow for clearer and more structured error reporting.

```jsx
error NotYourPokémon(address caller, uint pokeId);

function release(uint pokeId) public {
    if (pokémon[pokeId].trainer != msg.sender) {
        revert NotYourPokémon(msg.sender, pokeId);
    }
    // release logic
}


// Custom errors save gas by avoiding long revert strings and provide typed error handling.

```

## Modifier Functions

Modifiers are reusable code blocks that run **before** (and optionally after) a function executes. They're commonly used for access control, validations, or pausing logic.

```jsx
modifier onlyTrainer(uint pokeId) {
    require(pokémon[pokeId].trainer == msg.sender, "Not your Pokémon!");
    _;
}

function evolve(uint pokeId) public onlyTrainer(pokeId) {
    // Evolution logic
}


```

## 🧭 What’s Next?
You’ve mastered control and battle logic. Up next: Events and Logging — how your Pokémon contract sends messages to Trainers, logs wins, and keeps your Pokédex up to date .

