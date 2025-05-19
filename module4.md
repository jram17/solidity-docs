# 4. Functions and visibility
**Functions** are the core building blocks of any smart contract. They define the logic, manage data flow, and interact with users, other contracts, and the Ethereum Virtual Machine (EVM). Understanding how to define functions, manage access through visibility, and control behavior with modifiers is essential for writing secure and efficient contracts.

**Battle Functions Unlocked — Teach Your Pokémon to Fight!**
Now that your Pokémon has stats and identity, it’s time to train it to **battle**. Functions are the **moves** your Pokémon learns — they define how your smart contract behaves, how it responds to trainers (users), and how it interacts with other Pokémon (contracts) in the Ethereum region.

Just like different Pokémon have different move sets and strengths, Solidity functions have **visibility levels** and **modifiers** that control **who can use them**, **when**, and **how they interact** with the blockchain state or Ether.

In this module, you’ll learn:

-   How to define and use functions
-   How to control access using visibility keywords
 
-   How to optimize behavior with modifiers like `view`, `pure`, and `payable`
    
-   How to initialize your contract using a constructor — the moment your Pokémon hatches!

## Function Definitions
A function in Solidity is declared using the `function` keyword, followed by a name, parameters, visibility, and optional modifiers.

```jsx
function functionName([parameters]) [visibility] [modifiers] returns ([returnType]) {
    // code
}

```

```jsx
function transfer(address recipient, uint amount) public returns (bool) {
    // function logic
    return true;
}
```

### Visibility Keywords

Visibility determines **where** and **how** a function can be accessed. Solidity provides four visibility specifiers:

Visibility Keywords
| Visibility | Accessible From               | Use Case                          |
|------------|-------------------------------|-----------------------------------|
| `public`   | Anywhere                      | External and internal calls       |
| `private`  | Inside the same contract      | Internal utility functions        |
| `internal` | This and derived contracts    | Inheritance-based internal logic  |
| `external` | Only from outside the contract| Public API interface              |

```jsx
contract Example {
    function internalLogic() private { /* ... */ }
    function update() public { /* ... */ }
    function query() external view returns (uint) { /* ... */ }
}

//Best practice: Minimize use of public where not needed to limit attack surface.

```

## Function Modifiers
Function modifiers define how a function behaves with respect to the blockchain state and interaction with Ether.
| Modifier  | Description                                      |
|-----------|--------------------------------------------------|
| `view`    | Function reads from the blockchain state (no writes) |
| `pure`    | Function does not read or write state            |
| `payable` | Function can receive Ether                       |
```jsx
function getBalance() public view returns (uint) {
    return address(this).balance;
}

function calculate(uint a, uint b) public pure returns (uint) {
    return a + b;
}

function deposit() public payable {
    // Accepts Ether
}
```

## Constructors
A **constructor** is a special function that runs **once**, when the contract is deployed. It is typically used to initialize state variables or perform setup logic.

-   Declared using the `constructor` keyword.
-   Cannot be called again after deployment.

```jsx
contract Owned {
    address public owner;

    constructor() {
        owner = msg.sender;
    }
}

// Use constructors to assign roles, initial values, or immutable variables at deployment.
```

