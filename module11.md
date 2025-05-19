# 11. Bonus Module: Advanced Solidity Concepts
This module introduces essential standards and security patterns that are foundational for building secure and scalable smart contracts in real-world applications. it covers reentrancy protection, access control mechanisms, and a brief introduction to smart contract upgradeability via proxies.


## Security & Master Trainer Ranks

**You’re now facing gym leaders—security is key!**
Access control ensures that only authorized accounts can call sensitive functions, helping protect ownership, funds, and administrative actions in a contract.  
Just like gym badges grant access to new regions, Solidity access patterns restrict or unlock powerful contract features.  
Without proper access checks, even a low-level trainer could take control of your Legendary Pokémon—or worse, your contract’s Ether!
## Access Control Patterns

Access control ensures that only authorized accounts can call sensitive functions, helping protect ownership, funds, and administrative actions in a contract.

### `onlyOwner` using OpenZeppelin

A common pattern is to restrict access to the contract owner using OpenZeppelin’s `Ownable` module:

```jsx
import "@openzeppelin/contracts/access/Ownable.sol";

contract Vault is Ownable {
    function withdraw() public onlyOwner {
        // Only the deployer (or assigned owner) can execute
    }
}

```

## Custom Role-Based Access with `msg.sender`

For more granular control, you can define custom roles by comparing `msg.sender` to pre-set admin addresses:

```jsx
address public admin;

constructor() {
    admin = msg.sender;
}

modifier onlyAdmin() {
    require(msg.sender == admin, "Not authorized");
    _;
}

function pauseContract() public onlyAdmin {
    // Only admin can pause the contract
}

```

>💡 **You can expand this pattern using OpenZeppelin’s `AccessControl` for multi-role systems (e.g., MINTER_ROLE, PAUSER_ROLE).**

</aside>

## Reentrancy & Checks-Effects-Interactions Pattern

### What is Reentrancy?

Reentrancy is a **critical security vulnerability** where a malicious contract repeatedly calls a function **before the first invocation finishes**, often allowing unauthorized withdrawal of funds.

```jsx
function withdraw() public {
    require(balances[msg.sender] > 0);
    payable(msg.sender).call{value: balances[msg.sender]}("");
    balances[msg.sender] = 0; // too late!
}

```

The attacker can re-enter `withdraw()` before their balance is cleared.

### Checks-Effects-Interactions Pattern:

To prevent this, always update the state before making external calls to untrusted contracts

```jsx
function withdraw() public {
    uint amount = balances[msg.sender];
    require(amount > 0);

    balances[msg.sender] = 0; // Effects before external call
    payable(msg.sender).transfer(amount); // Interaction last
}

```

## Smart Contract Upgradeability (Intro to Proxies)

Once deployed, a smart contract is **immutable**. But in production systems, developers often need to **fix bugs** or **add new features**. This is where upgradeability comes in.

## Proxy Pattern Overview

A **proxy contract** delegates calls to a **logic (implementation) contract**, while keeping the same address and state.

**Common Proxy Standards:**

-   **Transparent Proxy (OpenZeppelin)**: Separates admin logic from user interaction.
-   **UUPS Proxy**: More gas efficient, supported by OpenZeppelin.

**Basic Idea:**

-   Proxy holds state.
-   Logic contract holds code.
-   When you want to upgrade, deploy a new logic contract and point the proxy to it.