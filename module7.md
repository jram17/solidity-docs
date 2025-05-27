# 7. Ether & Payments
> Poké Marts, Rare Candies, and Trainer Trades: Welcome to the Economy!

Your Pokémon are trained, your stats are stored… but what good is all that power without a way to evolve, trade, and buy items like Poké Balls or Rare Candies? Just like in the Pokémon world, money—or in our case, Ether—powers the entire ecosystem.

In this module, you’ll learn how to:
- Let Trainers deposit Ether into your contract
- Build a Poké Mart where they can buy items
- Implement safe, modern payment logic
- Handle Ether withdrawals and battle rewards
- Master the financial anatomy of a smart contract



Smart contracts on Ethereum can hold, send, and receive Ether. This module covers the fundamentals of handling Ether securely and efficiently within Solidity, including **payable functions**, **transaction context variables**, and **safe payment practices**.

## Payable functions

To let Trainers send Ether to your smart contract (whether to evolve a Pokémon or buy items), your function must be marked with the `payable` modifier.

```jsx
function evolvePokemon(uint pokemonId) public payable {
    require(msg.value >= 0.05 ether, "Evolution costs 0.05 ETH");
    // Trigger evolution animation here!
}

//  Use payable only when the function is explicitly meant to handle funds.

```

-   Only `payable` functions can receive Ether in a transaction.
-   If you send Ether to a non-payable function, the transaction will **revert**.

## Transaction Context Variables

Solidity provides several special global variables to handle Ether transactions:
| Variable                 | Description                                       |
|--------------------------|---------------------------------------------------|
| `msg.sender`             | Address of the caller (who initiated the call)    |
| `msg.value`              | Amount of Ether (in wei) sent with the call       |
| `address(this).balance`  | Ether balance of the current contract             |
These variables are critical in building payment logic and validating conditions such as minimum deposit amounts.

Example:
```jsx
function donateToGym() public payable {
    require(msg.value >= 0.01 ether, "Minimum donation is 0.01 ETH");
    emit GymFunded(msg.sender, msg.value);
}

```

## Sending Ether : Safe Ways to Reward Your Champions

There are three main methods for sending/transferring Ether from a contract:

1.  **Transfer**
    
    The transfer method is a straightforward and **legacy-recommended** way to send Ether.
    
    -   Forwards a **fixed 2,300 gas stipend**, just enough to allow a simple `receive` or `fallback` function.
    -   **Automatically reverts** if the transfer fails.
    -   Helps protect against reentrancy, but is **no longer reliable** for interacting with more complex contracts due to evolving gas costs.
    
    ```jsx
    payable(trainer).transfer(1 ether);
    
    ```


    
2.  **Send**
    
    The send method is similar to `transfer`, but **does not automatically revert** on failure. Instead, it returns a boolean indicating success.
    
    -   Forwards the same **2,300 gas**.
    -   Requires **explicit error checking** with `require`.
    
    ```jsx
    bool sent = payable(trainer).send(1 ether);
    require(sent, "Failed to send reward");

    
    ```
    
3.  **Call**
    
    The `call` method is now the **preferred** and most flexible way to send Ether, especially in modern smart contract development.
    
    -   Forwards **all remaining gas** by default.
    -   Returns a tuple: `(success, returnData)`.
    -   Can call arbitrary functions or just send Ether.
    
    ```jsx
    (bool success, ) = trainer.call{value: 1 ether}("");
    require(success, "Failed to send Ether via call");

    
    ```
    

## Withdrawal Pattern vs Direct Payments

### Direct Payment (Push Model)

-   Ether is sent during execution automatically.
-   If the recipient contract fails or rejects the payment, it can cause a complete transaction failure.

### Withdrawal Pattern (Pull Model)

Instead of “pushing” Ether to trainers (which can fail or be unsafe), use the pull pattern. Think of it like putting a PokéMart credit in their wallet, which they can redeem anytime.


-   Ether is **stored in the contract** until the recipient **manually withdraws it**.
-   Safer and minimizes risks of re-entrancy or failure in external contract logic.

```jsx
mapping(address => uint) public pendingRewards;

function rewardChampion(address winner) internal {
    pendingRewards[winner] += 1 ether;
}

function claimReward() public {
    uint amount = pendingRewards[msg.sender];
    require(amount > 0, "No rewards to claim");
    pendingRewards[msg.sender] = 0;

    (bool success, ) = msg.sender.call{value: amount}("");
    require(success, "Reward claim failed");
}


// Best Practice: Use the Withdrawal Pattern for sending Ether to unknown or untrusted addresses.

```

## 🧭 What’s Next?

Your contract can now accept and send Ether like a pro trainer handling PokéCoins—but how do you track what’s happening, notify users, or create a battle log of all your Pokémon fights, trades, and item purchases?

Coming up next:

Module 8 – Events and Logging

Every Pokémon battle needs a commentator! Learn how to emit events, log transactions, and create a transparent trail of activity for trainers and dApp frontends to follow
