# 2. Solidity syntax and structure

In this module, you’ll explore how a smart Pokémon is structured using Solidity. Think of this as designing your Pokémon’s DNA. Every smart Pokémon you build — from Bulbazar to Flareosaur — starts with a clean, structured contract.

Before your Pokémon can evolve, you must master the language that creates them.

**🎯 Objective**
> Master the building blocks of a smart Pokémon contract
Learn to write clean, maintainable Solidity code
Understand file structure, contract layout, and best practices

## Anatomy of a Pokémon Contract: .sol File Structure
When creating a smart Pokémon, your Solidity file (.sol) acts like its Pokédex entry—everything about your Pokémon is defined here!

1.  **SPDX License Identifier** – Declares the contract license (a trainer must play fair!)
2.  **Pragma directive** –  Tells the compiler which Solidity version your Pokémon speaks
3.  **Import statements** (if any) – Bring in shared items, Pokéballs (libraries) from other trainers
4.  **Contract declarations** – The core of the logic, This is where your Pokémon is born
5.  **Functions, state variables, modifiers, events, and constructors** - These define your Pokémon’s stats, moves, and behaviors

## Pragma and SPDX License

**SPDX-License-Identifier**
> Before you send your Pokémon into battle, register it properly!


This comment helps developers and platforms identify the software license for the contract:

```jsx
// SPDX-License-Identifier: MIT
```

-   Required by tools like **Remix** and **Hardhat**
-   Common licenses include: `MIT`, `GPL-3.0`, `Apache-2.0`



**Pragma solidity**

The `pragma` directive tells the compiler which version of Solidity the code is compatible with:

```jsx
pragma solidity ^0.8.20;
```

-   `^0.8.20` means any version from 0.8.20 up to (but not including) 0.9.0
-   Ensures compatibility and prevents accidental compilation with an unsupported version

**Other Valid Forms of pragma:**

| Syntax                            | Meaning                                        |
| --------------------------------- | ---------------------------------------------- |
| `pragma solidity ^0.8.0;`         | Compatible with 0.8.0 and up (excluding 0.9.0) |
| `pragma solidity >=0.8.0 <0.9.0;` | Explicit version range                         |
| `pragma solidity 0.8.20;`         | Strictly require version 0.8.20                |
| `pragma solidity >=0.7.0;`        | Any version starting from 0.7.0 and above      |
| `pragma solidity >=0.6.0 <0.8.0;` | Allow only a specific version range            |

> **Always specify a safe and tested compiler range to avoid unexpected behavior from future versions.**

> **Always place SPDX and the Pragma directive on the top of the file.**

## Contract Structure
Here’s a basic structure of a smart contract:
```jsx
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ExampleContract {
    
    // 1. State Variables
    address public owner;

    // 2. Events
    event OwnershipTransferred(address indexed previousOwner, address indexed newOwner);

    // 3. Modifiers
    modifier onlyOwner() {
        require(msg.sender == owner, "Not owner");
        _;
    }

    // 4. Constructor
    constructor() {
        owner = msg.sender;
    }

    // 5. Functions
    function transferOwnership(address newOwner) public onlyOwner {
        emit OwnershipTransferred(owner, newOwner);
        owner = newOwner;
    }
}

```

**Key Sections:**
-   **State Variables**: Hold contract data
-   **Constructor**: Runs once during deployment
-   **Modifiers**: Reusable logic that wraps functions
-   **Functions**: Define behavior and logic
-   **Events**: Log activity for off-chain tracking 

### Your First Smart Pokémon Contract
> Here’s what a simple contract looks like—it’s like designing your very first digital Charmander:
```jsx
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Charmander {
    
    // State Variable: stores Pokémon's current trainer
    address public trainer;

    // Event: logs when Charmander changes hands
    event NewTrainer(address indexed oldTrainer, address indexed newTrainer);

    // Modifier: only the current trainer can issue commands
    modifier onlyTrainer() {
        require(msg.sender == trainer, "You are not Charmander's trainer!");
        _;
    }

    // Constructor: Called once when Charmander is born
    constructor() {
        trainer = msg.sender;
    }

    // 🛠️ Function: Allows trainer to transfer ownership
    function transferTrainer(address newTrainer) public onlyTrainer {
        emit NewTrainer(trainer, newTrainer);
        trainer = newTrainer;
    }
}
```

## Comments and Formatting Best Practices
**Comments:**

-   Use **single-line comments** (`//`) for brief explanations.
-   Use **multi-line comments** (`/** ... */`) for functions, complex logic, or documentation.
-   Keep comments clear, relevant, and up to date.

**Formatting:**

-   Follow consistent **indentation** (typically 4 spaces).
-   Group related functions logically (e.g., state, getters, setters).
-   Keep functions short and focused.
-   Use whitespace to separate code blocks for readability.

## What's Next?
You’ve just taken your first step into the world of Solidity—and your Pokémon is born!

In the next module, you’ll learn how to give your Pokémon traits and attributes using Solidity Data Types. Think of this as assigning HP, Attack, XP, and more.
> “The journey of a thousand Pokémon starts with a single contract.” – Professor Oak
