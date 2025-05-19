# 9. Inheritance, Interfaces, and Libraries
**Pokémon Families**--Define Pokémon types and abilities via inheritance.
As smart contracts grow in complexity, **code reuse, modularity, and abstraction** become essential. Solidity supports robust object-oriented programming features like **inheritance**, **interfaces**, and **libraries**, which enable developers to write clean, reusable, and maintainable code.

This module explores how these features work and introduces trusted tools like **OpenZeppelin** to streamline development.


## Contract Inheritance
Solidity supports **single and multiple inheritance**, allowing contracts to inherit functions, modifiers, and state variables from parent contracts.

```jsx
contract Base {
    function greet() public pure returns (string memory) {
        return "Hello";
    }
}

contract Derived is Base {
    // Inherits greet() from Base
}

```

**Key Benefits:**

-   Encourages modular contract design
-   Reduces code duplication
-   Enables access control patterns and reusable logic

Using `abstract`, `virtual`, and `override`

Inheritance in Solidity is tightly coupled with **polymorphism** through the use of the `virtual` and `override` keywords.

-   **virtual**: Marks a function as overridable by child contracts.
-   **override**: Indicates a function is replacing a virtual function from a parent.

```jsx
contract Animal {
    function speak() public pure virtual returns (string memory) {
        return "Some sound";
    }
}

contract Dog is Animal {
    function speak() public pure override returns (string memory) {
        return "Woof!";
    }
}

```

-   **abstract** contracts are used when a contract contains at least one function without implementation. These cannot be deployed directly.

```jsx
abstract contract Animal {
    function move() public virtual;
}

// Use abstract contracts and virtual functions to define base behavior, then implement it in child contracts for clarity and flexibility.


```

## Interfaces in Solidity

Interfaces define **external contract behavior** without implementing it. They're used to interact with other contracts, particularly for standardization (e.g. ERC-20, ERC-721).

### Key Rules:

-   Only function declarations allowed (no logic)
-   All functions must be `external`
-   Cannot declare state variables

```jsx
interface IToken {
    function transfer(address to, uint amount) external returns (bool);
}

```

Interfaces allow contracts to **communicate across systems** while adhering to predefined standards—critical in DeFi and token ecosystems.

### Libraries and OpenZeppelin

Libraries in Solidity are reusable units of logic that help developers keep contracts modular and gas-efficient. Functions in libraries are called **without copying code** into the contract using `delegatecall`.

Using OpenZeppelin Utilities

OpenZeppelin provides a widely-used, audited set of contracts and libraries for:

-   Access control (`Ownable`, `AccessControl`)
-   Tokens (`ERC20`, `ERC721` , `ERC1155`)
-   Utilities (`SafeMath`, `Counters`, `ReentrancyGuard`)

### Benefits:

-   Security-reviewed code
-   Standard implementations (e.g., ERCs)
-   Easy integration with tools like Hardhat and Foundry

Example

```jsx
import "@openzeppelin/contracts/access/Ownable.sol";

contract Vault is Ownable {
    function withdraw() public onlyOwner {
        // only the contract owner can call this
    }
}
```