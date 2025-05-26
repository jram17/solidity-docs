# 3. Data types and variables
> **Add Stats and Identity to Your Pokémon**

You’ve summoned your smart Pokémon into existence with Solidity—but a name isn’t enough. To battle in the Ethereum region, your Pokémon needs stats like HP, Type, and Power Level. It needs a Pokédex profile coded in Solidity’s data types.

In this module, you'll learn how to give your Pokémon its identity, abilities, and background data using Solidity’s value types, reference types, and variable scopes.

## 🎯 Mission Objective
- Understand how to store and manage Pokémon data
- Learn value types, reference types, and variable scopes
- Discover constants and immutables for efficient stats

## Value Types
Value types are stored directly in memory and passed by value (i.e., copies are made). Solidity provides several built-in value types:

| Type      | Description                        | Example                          | Pokémon Use Case                                        |
| --------- | ---------------------------------- | -------------------------------- | ------------------------------------------------------- |
| `uint`    | Unsigned integer (e.g., `uint256`) | `uint256 power = 25;`              | Set a Pokémon’s `hp`, `level`, or `attack power`.       |
| `int`     | Signed integer                     | `int256 temperature = -5;`       | Used for elemental Pokémon with cold or hot attacks.    |
| `bool`    | Boolean value (`true` or `false`)  | `bool isActive = true;`          | Track whether a Pokémon is in battle or fainted.        |
| `address` | Ethereum address (20-byte value)   | `address user = msg.sender;`     | Identify the Pokémon’s trainer (wallet address).        |
| `bytes32` | Fixed-size 32-byte array           | `bytes32 hash = keccak256(...);` | Store unique DNA hash or evolution IDs.                 |
| `string`  | UTF-8 encoded dynamic-length text  | `string name = "ditto";`         | Name your Pokémon, describe its type or evolution path. |


## Reference Types
Reference types store locations in memory or storage, not the actual data. They are more complex and require careful handling.
1.  Arrays
    
    -  Fixed or dynamic-size lists
        
        ```jsx
        uint[] public scores;
        string[] public moveSet = ["Ember", "Roar", "Tackle"];
        
        ```
        
2.  Mappings
    
    -  Key-value store; commonly used for efficient data lookup
        
        ```jsx
        mapping(address => uint) public xpEarned;
        
        ```
        
3.  Structs
    
    -  Custom data types that group related variables
        
        ```jsx
        struct Pokemon {
            string name;
            uint hp;
            string pokeType;
            bool isLegendary;
        }
        
        ```


## Variable scopes : Where Do Pokémon Store Their Memories?
Just like Pokémon remember moves differently during battle .In Solidity, variables exist in different **scopes**, which define how and where the data is stored and accessed during contract execution. Understanding these scopes is essential for writing efficient and secure smart contracts.

1.  State variable
    
    -   Declared **outside** functions.
    -   Stored **permanently on the blockchain** (in contract storage).
    -   Cost **gas** to read/write (except when accessed via `view` or `pure` functions).
    
    ```jsx
    string public species = "Charmander";; // state variable
    
    //Used to persist data across function calls and contract executions.
    
    ```
    
2.  Local variable
    
    -   Declared **inside functions**.
    -   Exist **temporarily during function execution**.
    -   Stored in **memory** or **stack**, depending on type.
    -   **Do not** cost gas unless interacting with storage or performing operations that consume gas.
    
    ```jsx
    function battleDamage(uint base, uint multiplier) public pure returns (uint) {
        uint result = base * multiplier;
        return result;
    }
    
    //Ideal for intermediate calculations or temporary values.
    
    ```
    
3.  Global variable
    
    -   Built-in variables provided by the **EVM context**.
    -   Accessible anywhere in the contract.
    -   Provide information about the blockchain, transaction, or message.
    
| Global Variable     | Description                              |
|---------------------|------------------------------------------|
| `msg.sender`        | Address that initiated the call          |
| `msg.value`         | Amount of Ether sent with the call       |
| `block.timestamp`   | Current block’s timestamp                |
| `block.number`      | Current block number                     |
| `tx.origin`         | Original external account initiator      |


## 	Constant and Immutables : Unchangeable Pokémon Laws
> Some Pokémon stats never change. Solidity gives you two options to lock values.

Solidity allows the declaration of variables whose values never change, which improves **readability**, **security**, and **gas efficiency**.

1.  Constant
    
    -   Must be assigned **at compile time**.
    -   Typically used for values that will never change (e.g., max limits, conversion rates).
    -   Stored directly in the byte-code → **no storage cost**.
    
    ```jsx
    uint constant MAX_HP = 255;
    
    ```
    
2.  Immutable
    
    -   Assigned **once** during contract **deployment** (in the constructor).
    -   Useful for values that are dynamic at deployment (e.g., `owner`, configuration values).
    -   Stored in byte—code like `constant`, but initialized at runtime.
    
    ```jsx
       address immutable creator;

    constructor() {
        creator = msg.sender;
    }
    
    ```

##  What’s Next?
Now that you’ve programmed your Pokémon’s stats and memory, it’s time to give them behavior. In the next module, you’ll learn about:
> Functions, visibility, and control structures
  How to let your Pokémon battle, evolve, and interact with others on the blockchain
