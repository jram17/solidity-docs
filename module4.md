# 4. Functions and visibility
> **Battle Functions Unlocked — Teach Your Pokémon to Fight!**

Now that your Pokémon has stats and identity, it’s time to train it to **battle**. Functions are the **moves** your Pokémon learns — they define how your smart contract behaves, how it responds to trainers (users), and how it interacts with other Pokémon (contracts) in the Ethereum region.

Just like different Pokémon have different move sets and strengths, Solidity functions have **visibility levels** and **modifiers** that control **who can use them**, **when**, and **how they interact** with the blockchain state or Ether.

## 🎯 Mission Objective
-   Write reusable, well-scoped Solidity functions
-   Use visibility to control function access
 
-   Add behavioral modifiers like `view` , `pure` and `payable`
    
-   Hatch your Pokémon with a constructor

## Function Definitions
A function in Solidity is declared using the `function` keyword, followed by a name, parameters, visibility, and optional modifiers.

```jsx
function moveName([parameters]) [visibility] [modifiers] returns ([returnType]) {
    // Move logic
}

```

```jsx
function tackle(address enemy, uint damage) public returns (bool) {
    // Pokémon attacks another
    return true;
}
```

### Visibility Keywords - Who Can Use the Move?

Visibility determines **where** and **how** a function can be accessed. Just like some Pokémon can only use certain moves in specific battles, function visibility controls where and who can call the function.

Solidity provides four visibility specifiers:
Visibility Keywords
| Visibility | Accessible From               | Use Case                          |
|------------|-------------------------------|-----------------------------------|
| `public`   | Anywhere                      | External and internal calls       |
| `private`  | Inside the same contract      | Internal utility functions        |
| `internal` | This and derived contracts    | Inheritance-based internal logic  |
| `external` | Only from outside the contract| Public API interface              |

```jsx
contract Pikacode {
    function _zap() private { /* internal only */ }
    function thunderbolt() public { /* callable by users */ }
    function evolve() internal { /* shared by evolved forms */ }
    function trade() external { /* callable from outside only */ }
}


//Best practice: Minimize use of public where not needed to limit attack surface.

```

## Function Modifiers - Move Behavior Types
Function modifiers define how a function behaves with respect to the blockchain state and interaction with Ether.
| Modifier  | What It Means                             | Pokémon Analogy                    |
| --------- | ----------------------------------------- | ---------------------------------- |
| `view`    | Reads state only (doesn't write)          | Scanning opponent's stats          |
| `pure`    | Does not read or write any contract state | Internal calculations like damage  |
| `payable` | Accepts Ether from Trainers               | A move that costs Ether to perform |

```jsx
function getHP() public view returns (uint) {
    return currentHP;
}

function calculateDamage(uint atk, uint def) public pure returns (uint) {
    return atk - def;
}

function evolveWithMoonStone() public payable {
    require(msg.value >= 1 ether, "Not enough Ether");
    // Trigger evolution
}

```

## Constructors
Every Pokémon starts with a special moment — when it hatches and becomes part of your team. That’s what a constructor does in Solidity!

**Constructors** run once, at deployment, and are used to assign initial values, like your Pokémon’s trainer, origin story, or immutable traits.

-   Declared using the `constructor` keyword.
-   Cannot be called again after deployment.

```jsx
contract Charmantle {
    address public trainer;

    constructor() {
        trainer = msg.sender; // The first one to deploy becomes the Trainer
    }
}


// Use constructors to assign roles, initial values, or immutable variables at deployment.
```


## 🧭 What’s Next?
Get ready to dive into control flow and logic — the part of the contract that teaches your Pokémon how to make decisions in battle and beyond!



