# 2. Solidity syntax and structure

In this module, you’ll explore how a smart Pokémon is structured using Solidity. Think of this as designing your Pokémon’s DNA. Every smart Pokémon you build — from Bulbazar to Flareosaur — starts with a clean, structured contract.

Before your Pokémon can evolve, you must master the language that creates them.

**🎯 Objective**
Understand the syntax conventions, layout, and formatting best practices that define clean, readable, and maintainable Solidity contracts.
##  File Structure of a `.sol` File
A typical Solidity file (`.sol`) is a self-contained script that defines one or more smart contracts. Solidity files are structured from top to bottom with clearly defined sections:

1.  **Pragma directive** – Declares the compiler version
2.  **SPDX License Identifier** – Specifies the open-source license
3.  **Import statements** (if any) – Brings in external contracts or libraries
4.  **Contract declarations** – The core of the logic
5.  **Functions, state variables, modifiers, events, and constructors** – Defined inside contracts

## Pragma and SPDX License
**Pragma solidity**

The `pragma` directive tells the compiler which version of Solidity the code is compatible with:

```jsx
pragma solidity ^0.8.20;
```

-   `^0.8.20` means any version from 0.8.20 up to (but not including) 0.9.0
-   Ensures compatibility and prevents accidental compilation with an unsupported version

**SPDX-License-Identifier**

This comment helps developers and platforms identify the software license for the contract:

```jsx
// SPDX-License-Identifier: MIT
```

-   Required by tools like **Remix** and **Hardhat**
-   Common licenses include: `MIT`, `GPL-3.0`, `Apache-2.0`

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