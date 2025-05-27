

# 8. Events and Logging
> Trainer! Your Pokémon leveled up!

Just like announcements in a Pokémon battle — “It’s super effective!” or “Pikachu evolved!” — smart contracts need a way to broadcast key events to trainers and the outside world. That’s what events in Solidity do.

Events act like a Pokémon commentator, narrating what’s happening on the blockchain so your front-end apps, explorers, and tracking tools can follow the action.


This module covers what events are, how to emit and listen to them, and their impact on gas costs.

## What Are Events?
Events are signals your smart contract sends when something important happens: a trade, a victory, an evolution. They're not stored in the contract state but are recorded in the blockchain’s transaction logs, ready for front-end apps, explorers, and indexers to pick up.

They are primarily used to:

-   Notify off-chain systems of on-chain activity
-   Record state changes or user interactions
-   Enable blockchain explorers (like Etherscan) to display activity

```jsx
event Transferred(address indexed from, address indexed to, uint amount);

```

Here we use events for:
- Tracking battles, trades and stats updates
- Alerting trainers to real-time actions
- Feeding data to the Pokédex (a.k.a dApp UI)

```jsx
event BattleResult(address indexed trainer, string result, uint256 exp);

```





> Events are declared outside of functions, typically near the top of the contract.



## Emitting Events - "Trainer used Thunderbolt!"

Inside your contract, you emit events to log occurrences:

```jsx
event BattleResult(address indexed trainer, string result, uint256 exp);

```

This action stores the event in the transaction’s log, which is accessible via:

-   Web3.js / Ethers.js
-   Blockchain explorers
-   Indexing tools like The Graph

## Listening Off-Chain - "Announcer mode: ON"

Using tools like Web3.js or Ethers.js, your dApp can “listen” for these on-chain shouts:

```jsx
contract.events.BattleResult({
  filter: { trainer: userAddress },
  fromBlock: 'latest'
}, (err, event) => {
  console.log("📢 Battle log:", event.returnValues);
});

```

This integration enables dynamic interfaces and notifications, bridging smart contracts with real-world applications.

## Indexed Parameters

Solidity allows up to **3 parameters** in an event to be marked as `indexed`. These indexed fields are stored in a **Bloom filter**, making them searchable when filtering logs.

```jsx
event Traded(address indexed fromTrainer, address indexed toTrainer, uint pokemonId);

```

**Benefits of Indexed Parameters:**

-   Enable efficient filtering by topics (e.g., find all events from a specific address)
-   Improve query performance when scanning large log datasets

> 💡 You can have more than 3 parameters, but only the first 3 can be indexed.


**Gas Implications of Events**

-   Emitting an event **costs gas**, but it’s **cheaper than writing to storage**.
-   The cost includes:
    -   A fixed base cost for logging
    -   A cost per topic (i.e., indexed parameter)
    -   A cost per byte of data

### **Why use events?**

-   Events are stored in **transaction logs**, not state, so they don’t increase long-term storage costs.
    
-   This makes them **ideal for off-chain notification**, but **not reliable for on-chain logic** (smart contracts cannot read past event logs).
    
 
> 💡 **Use events to signal meaningful actions: deposits, transfers, ownership changes ,but not as a substitute for state.**
    
## 🧭 What’s Next?
You’ve just learned how to broadcast battles and evolutions like a seasoned announcer—now it’s time to level up your contracts themselves.

Next up:

 Module 9 — Inheritance, Interfaces, and Libraries: Build Your Contract Pokédex

Just like Pokémon inherit traits from their types and abilities, smart contracts can inherit code and share logic. Discover how to build modular, reusable, and interconnected contract systems — your very own Pokémon species hierarchy.
