# 3. Data types and variables
**Add Stats and Identity to Your Pokémon**
To truly bring your Pokémon to life on the blockchain, it needs more than just a name. It needs **stats**, **traits**, and **a profile** that defines its uniqueness—just like in your Pokédex!

In this module, you'll learn how to define these characteristics using Solidity's core data types. You'll create Pokémon identities with attributes like `hp`, `type`, `strength`, and manage them using proper variable scope and memory efficiency.

## Value Types
Value types are stored directly in memory and passed by value (i.e., copies are made). Solidity provides several built-in value types:

| Type    | Description                          | Example                          |
|---------|--------------------------------------|----------------------------------|
| `uint`  | Unsigned integer (e.g., `uint256`)   | `uint256 age = 25;`              |
| `int`   | Signed integer                       | `int256 temperature = -5;`       |
| `bool`  | Boolean value (`true` or `false`)    | `bool isActive = true;`          |
| `address` | Ethereum address (20-byte value)   | `address user = msg.sender;`     |
| `bytes` | Fixed-size byte arrays (e.g., `bytes32`) | `bytes32 hash = keccak256(...);` |
| `string`| UTF-8 encoded dynamic text           | `string name = "Alice";`         |


## Reference Types
Reference types store locations in memory or storage, not the actual data. They are more complex and require careful handling.
1.  Arrays
    
    -  Fixed or dynamic-size lists
        
        ```jsx
        uint[] public scores;
        string[3] public topUsers;
        
        ```
        
2.  Mappings
    
    -  Key-value store; commonly used for efficient data lookup
        
        ```jsx
        mapping(address => uint) public balances;
        
        ```
        
3.  Structs
    
    -  Custom data types that group related variables
        
        ```jsx
        struct Profile {
            string name;
            uint age;
            bool verified;
        }
        
        ```


## Variable scope in solidity
In Solidity, variables exist in different **scopes**, which define how and where the data is stored and accessed during contract execution. Understanding these scopes is essential for writing efficient and secure smart contracts.

1.  State variable
    
    -   Declared **outside** functions.
    -   Stored **permanently on the blockchain** (in contract storage).
    -   Cost **gas** to read/write (except when accessed via `view` or `pure` functions).
    
    ```jsx
    uint public totalUsers; // state variable
    
    //Used to persist data across function calls and contract executions.
    
    ```
    
2.  Local variable
    
    -   Declared **inside functions**.
    -   Exist **temporarily during function execution**.
    -   Stored in **memory** or **stack**, depending on type.
    -   **Do not** cost gas unless interacting with storage or performing operations that consume gas.
    
    ```jsx
    function calculate(uint a, uint b) public pure returns (uint) {
        uint sum = a + b; // local variable
        return sum;
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


## 	Constant and Variables
Solidity allows the declaration of variables whose values never change, which improves **readability**, **security**, and **gas efficiency**.

1.  Constant
    
    -   Must be assigned **at compile time**.
    -   Typically used for values that will never change (e.g., max limits, conversion rates).
    -   Stored directly in the byte-code → **no storage cost**.
    
    ```jsx
    uint constant MAX_USERS = 100;
    
    ```
    
2.  Immutable
    
    -   Assigned **once** during contract **deployment** (in the constructor).
    -   Useful for values that are dynamic at deployment (e.g., `owner`, configuration values).
    -   Stored in byte—code like `constant`, but initialized at runtime.
    
    ```jsx
    address immutable owner;
    
    constructor() {
        owner = msg.sender;
    }
    
    ```