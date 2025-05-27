# 9. Inheritance, Interfaces, and Libraries
> Pokémon Families – Sharing Traits Across Generations

As your Pokémon world expands, you’ll need to define types, shared abilities, and common behaviors across Pokémon species. Think of inheritance as evolution paths, interfaces as battle protocols, and libraries as shared Pokédex knowledge. This module helps you harness the power of modularity, code reuse, and standardized battle rules with Solidity’s advanced programming constructs.


## Contract Inheritance
Just like how Pikachu and Raichu share electric powers, Solidity contracts can inherit abilities from their ancestors. Inheritance helps you organize code, reduce duplication, and evolve contracts over time.

```jsx
contract Pokemon {
    function typeOf() public pure returns (string memory) {
        return "Electric";
    }
}

contract Pikachu is Pokemon {
    // Pikachu inherits typeOf from Pokemon
}

```

**Key Benefits:**

-   Encourages modular contract design
-   Reduces code duplication
-   Enables access control patterns and reusable logic

## Using `abstract`, `virtual`, and `override`

Sometimes your base Pokémon is incomplete—like a fossil waiting to be revived. Use abstract contracts to define a blueprint, and virtual/override to customize behavior in derived Pokémon

```jsx
abstract contract Creature {
    function speak() public virtual returns (string memory);
}

contract Psyduck is Creature {
    function speak() public pure override returns (string memory) {
        return "Psy-ai-ai!";
    }
}

```

> Abstract = Blueprint Pokémon

> Virtual = "This move can evolve."

> Override = "I’ve evolved this move."



## Interfaces in Solidity
Interfaces act like battle protocols: every Pokémon that wants to fight in a league must implement the right moves. They don’t define how the moves work—just that they must exist.


### Key Rules:

-   Only function declarations allowed (no logic)
-   All functions must be `external`
-   Cannot declare state variables

```jsx
interface IBattleReady {
    function attack(address target) external;
    function defend() external returns (bool);
}


```

Interfaces allow contracts to **communicate across systems** while adhering to predefined standards—critical in DeFi and token ecosystems.

### Libraries and OpenZeppelin

Libraries are non-deployable contracts packed with reusable moves. Use them to teach all your Pokémon utility logic like calculating damage or managing cooldowns.

### Example : Utility Library
```jsx
library DamageCalculator {
    function calculate(uint base, uint multiplier) internal pure returns (uint) {
        return base * multiplier;
    }
}

```

```jsx
import "./DamageCalculator.sol";

contract Battle {
    using DamageCalculator for uint;

    function strike(uint base, uint power) public pure returns (uint) {
        return base.calculate(power); // uses library logic
    }
}

```

## OpenZeppelin - Trusted Pokémon Professor Tools 

OpenZeppelin is like Professor Oak’s lab—packed with tools and wisdom for smart trainers.

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

contract PokéVault is Ownable {
    function withdraw() public onlyOwner {
        // only Ash can withdraw rare candies
    }
}

```


## 🧭 What’s Next?

You’ve now designed evolutionary chains, standardized Pokémon interactions, and equipped your team with shared moves from trusted libraries.You’ve now designed evolutionary chains, standardized Pokémon interactions, and equipped your team with shared moves from trusted libraries.

Coming up Next :

Module 10 – Token Standards: Train Your Pokémon as Tradable Assets!

It's time to mint your own Pokémon cards! Learn how to implement ERC-20 for fungible items like PokéCoins, and ERC-721 or ERC-1155 for unique Pokémon and items. Turn your contracts into fully tradable, collectible assets on the blockchain!


