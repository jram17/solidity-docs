

# 8. Events and Logging
Broadcast major Pokémon events—evolutions, wins, and losses!
Events in Solidity are a powerful feature that allows smart contracts to log meaningful information to the blockchain. These logs can be **accessed off-chain** by external consumers (like web applications or backend services) and serve as a key mechanism for **tracking contract activity**.

This module covers what events are, how to emit and listen to them, and their impact on gas costs.

## What Are Events?

Events are user-defined **logging mechanisms** in Solidity. When an event is emitted, the data is **written to the blockchain log**, but **not stored in contract storage**, making them efficient for external tracking.

They are primarily used to:

-   Notify off-chain systems of on-chain activity
-   Record state changes or user interactions
-   Enable blockchain explorers (like Etherscan) to display activity

```jsx
event Transferred(address indexed from, address indexed to, uint amount);

```

Events are declared outside of functions, typically near the top of the contract.

Emitting and Listening to Events

## Emitting Events

Inside your contract, you emit events to log occurrences:

```jsx
emit Transferred(msg.sender, recipient, amount);

```

This action stores the event in the transaction’s log, which is accessible via:

-   Web3.js / Ethers.js
-   Blockchain explorers
-   Indexing tools like The Graph

## Listening Off-Chain

Client applications (e.g. using Web3.js) can listen for events like this:

```jsx
contract.events.Transferred({
  filter: { from: userAddress },
  fromBlock: 'latest'
}, function(error, event) {
  console.log(event.returnValues);
});

```

This integration enables dynamic interfaces and notifications, bridging smart contracts with real-world applications.

## Indexed Parameters

Solidity allows up to **3 parameters** in an event to be marked as `indexed`. These indexed fields are stored in a **Bloom filter**, making them searchable when filtering logs.

```jsx
event ItemListed(address indexed seller, uint indexed itemId, uint price);

```

**Benefits of Indexed Parameters:**

-   Enable efficient filtering by topics (e.g., find all events from a specific address)
-   Improve query performance when scanning large log datasets

<aside> 💡
You can have more than 3 parameters, but only the first 3 can be indexed.

</aside>

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
    
