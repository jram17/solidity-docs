# 11. Bonus Module: Advanced Solidity Concepts

You’ve caught them all—but can you protect them?

This final stage of your journey takes you deep into the security caves of Solidity and introduces you to evolutionary-level techniques like reentrancy protection, access control, and proxy-based upgradeability.

Welcome to the Elite Four of Smart Contract Development—where each bug could be a critical hit if you’re not prepared!



## Access Control – Your Gym Badges

You’re up against gym leaders now—security is not optional.
Access control is how we make sure only qualified trainers (owners, admins, or roles) can use powerful moves—like minting tokens, withdrawing funds, or updating contract logic.

Think of it as badges unlocking advanced features:

### `onlyOwner` using OpenZeppelin

Used for simple contracts where one trainer (the owner) holds all power:

```jsx
import "@openzeppelin/contracts/access/Ownable.sol";

contract PokéVault is Ownable {
    function withdrawPokéCoins() public onlyOwner {
        // Only the Champion can access the vault
    }
}


```

## The Custom Role Badge `(onlyAdmin)(msg.sender)`

For more granular control, you can define custom roles by comparing `msg.sender` to pre-set admin addresses:

```jsx
address public gymLeader;

constructor() {
    gymLeader = msg.sender;
}

modifier onlyLeader() {
    require(msg.sender == gymLeader, "You’re not a gym leader!");
    _;
}

function openBattleArena() public onlyLeader {
    // Only gym leaders can open the arena
}


```

>💡  For a full role system with multiple trainers, check out OpenZeppelin’s AccessControl (great for large-scale leagues).


## Reentrancy - Defending Against Ghost-Type Attacks

### What is Reentrancy?

> Reentrancy is a **critical security vulnerability** where a malicious contract repeatedly calls a function **before the first invocation finishes**, often allowing unauthorized withdrawal of funds.

It’s like a ghost Pokémon using Shadow Sneak—attacking before you finish your move.

```jsx
function withdraw() public {
    require(balances[msg.sender] > 0);
    payable(msg.sender).call{value: balances[msg.sender]}("");
    balances[msg.sender] = 0; // oops—too late!
}

```

> The attacker can re-enter `withdraw()` before their balance is cleared.

### Checks-Effects-Interactions Pattern:

To prevent this, always update the state before making external calls to untrusted contracts

```jsx
function withdraw() public {
    uint256 amount = balances[msg.sender];
    require(amount > 0);

    balances[msg.sender] = 0; // Effects first
    payable(msg.sender).transfer(amount); // Interaction last
}

```

## Upgradeability – Mega Evolution for Contracts

Once a contract is deployed, it’s like setting a Pokémon’s nature—it can’t change.
But in real-world apps, you may need to patch bugs or add new features.

This is where proxies come in.
Think of them as evolution stones—upgrading your logic without changing the Pokémon (contract address)!

## Proxy Pattern 

A **proxy contract** delegates calls to a **logic (implementation) contract**, while keeping the same address and state.
- Proxy = Pokémon (holds experience, stats, and location)
- Logic Contract = Move Tutor (defines what it can do)
- Want to teach a new move? Just switch the Move Tutor.



**Common Proxy Types : **

-   **Transparent Proxy (OpenZeppelin)**: Clean separation between user and admin actions.
-   **UUPS Proxy**:  Lighter and more gas-efficient (like Quick Attack!).

> With OpenZeppelin Upgrades, you can deploy and upgrade contracts with safety checks and minimal hassle

**Basic Idea:**

-   Proxy holds state.
-   Logic contract holds code.
-   When you want to upgrade, deploy a new logic contract and point the proxy to it.


## 🧭 What’s Next?
You’ve mastered the code, the security, and the upgrade mechanics.
Your PokéDeck is full, your contracts are armored—and your title of Solidity Champion is well-earned.

But this isn’t the end.
True champions give back, build dApps, audit projects, and evolve the ecosystem.

Until next season:
Go beyond! Train harder. Code smarter. And deploy boldly.
