
# 1. Introduction
Professor Oak’s Blockchain Lab
Welcome to **Professor Oak’s Blockchain Lab**, where the world of Pokémon begins! You're a new **blockchain trainer**, preparing to build and battle in the Ethereum region using smart contracts and Solidity.

Here’s what you’ll discover in this module:

## What is Solidity
Solidity is a **statically typed**, **contract-oriented** programming language designed specifically for writing **smart contracts** on Ethereum and compatible blockchain platforms. It is similar in syntax to JavaScript, with influences from C++ and Python.

Solidity allows developers to write business logic that runs on the Ethereum Virtual Machine (EVM), enabling decentralized, trust-less applications that run exactly as programmed.

 - Solidity files uses the .sol extension and are compiled into EVM byte-code before deployment.


##  What are Smart Contracts?
A **smart contract** is a self-executing program that runs on the blockchain. It defines a set of rules and outcomes, and once deployed, it automatically enforces those rules without the need for a central authority, intermediary, or manual oversight.

Smart contracts allow developers to build decentralized applications (dApps) that are:

-   **Trustless**: Parties don't need to trust each other—only the code.
-   **Transparent**: Code and execution results are publicly visible and verifiable on the blockchain.
-   **Immutable**: Once deployed, the contract’s logic cannot be changed.
-   **Autonomous**: Execution is triggered by transactions and runs without external intervention.

## Overview of the Ethereum Virtual Machine (EVM)
The **Ethereum Virtual Machine (EVM)** is the decentralized runtime environment that executes smart contracts on the Ethereum blockchain. It ensures that every node on the Ethereum network computes the same result from the same inputs—maintaining consensus across a global, trustless system.

In essence, the EVM is the engine that powers the Ethereum blockchain. It processes smart contract instructions, handles state changes, and performs computations securely and deterministically.

## Gas and Transaction fees
A transaction is a message that is sent from one account to another account (which might be the same or empty, see below). It can include binary data (which is called “payload”) and Ether.

Every operation on Ethereum . contract deployment,function calls, storage updates etc .requires computational resources . These are paid using gas

-   **Gas**: A unit of computation in the EVM
-   **Gas Price**: The amount of Ether a user is willing to pay per unit of gas (measured in gwei)
-   **Gas Limit**: The maximum gas the transaction can use
-   **Transaction Fee** = `Gas Used × Gas Price`

Gas ensures that network resources are used responsibly and protects the network from infinite loops or spam.

Smart contracts must be written efficiently to minimize gas consumption, especially for operations involving storage or loops.

