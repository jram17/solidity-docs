# 7. Ether & Payments
Pokémon evolution costs Ether—transactions and payments begin!
Smart contracts on Ethereum can hold, send, and receive Ether. This module covers the fundamentals of handling Ether securely and efficiently within Solidity, including **payable functions**, **transaction context variables**, and **safe payment practices**.

## Payable functions

To enable a function to **receive Ether**, it must be marked with the `payable` modifier

```jsx
function deposit() public payable {
    // Ether sent is now part of the contract's balance
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

## Sending Ether

There are three main methods for sending/transferring Ether from a contract:

1.  **Transfer**
    
    The transfer method is a straightforward and **legacy-recommended** way to send Ether.
    
    -   Forwards a **fixed 2,300 gas stipend**, just enough to allow a simple `receive` or `fallback` function.
    -   **Automatically reverts** if the transfer fails.
    -   Helps protect against reentrancy, but is **no longer reliable** for interacting with more complex contracts due to evolving gas costs.
    
    ```jsx
    payable(recipient).transfer(1 ether);
    
    ```
    
2.  **Send**
    
    The send method is similar to `transfer`, but **does not automatically revert** on failure. Instead, it returns a boolean indicating success.
    
    -   Forwards the same **2,300 gas**.
    -   Requires **explicit error checking** with `require`.
    
    ```jsx
    bool success = payable(recipient).send(1 ether);
    require(success, "Send failed");
    
    ```
    
3.  **Call**
    
    The `call` method is now the **preferred** and most flexible way to send Ether, especially in modern smart contract development.
    
    -   Forwards **all remaining gas** by default.
    -   Returns a tuple: `(success, returnData)`.
    -   Can call arbitrary functions or just send Ether.
    
    ```jsx
    (bool success, ) = recipient.call{value: 1 ether}("");
    require(success, "Call failed");
    
    ```
    

## Withdrawal Pattern vs Direct Payments

### Direct Payment (Push Model)

-   Ether is sent during execution automatically.
-   If the recipient contract fails or rejects the payment, it can cause a complete transaction failure.

### Withdrawal Pattern (Pull Model)

-   Ether is **stored in the contract** until the recipient **manually withdraws it**.
-   Safer and minimizes risks of re-entrancy or failure in external contract logic.

```jsx
mapping(address => uint) public balances;

function deposit() public payable {
    balances[msg.sender] += msg.value;
}

function withdraw() public {
    uint amount = balances[msg.sender];
    require(amount > 0, "No balance");
    balances[msg.sender] = 0;

    (bool success, ) = msg.sender.call{value: amount}("");
    require(success, "Withdrawal failed");
}

// Best Practice: Use the Withdrawal Pattern for sending Ether to unknown or untrusted addresses.

```