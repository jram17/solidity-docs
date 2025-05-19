# 6. Structs, Mappings & Arrays
Solidity provides structured and efficient data types for organizing and managing data in smart contracts. This module introduces three essential composite types such as **structs**, **mappings**, and **arrays** and how to use them effectively.

## Structs : Custom Data Types

A struct is a user-defined data type that groups related variables into a single unit. Structs are useful for modeling entities such as user profiles, records, or metadata.

```jsx
struct User {
    string name;
    uint age;
    address wallet;
}

User public user;

```

Structs can be stored as:

-   **State variables** (persistent storage)
-   **Local variables** (in functions)
-   **Function parameters and return types**

## Mappings : Key-Value Storage

Mappings store key-value pairs and are commonly used for fast, efficient lookup.

```jsx
mapping(address => uint) public balances;

```

-   Keys can be of **value types** (e.g., `address`, `uint`, `bool`)
-   Values can be any type, including structs or arrays
-   **Mappings are not iterable**

Use Cases:

-   Token balances (`mapping(address => uint)`)
-   Ownership records
-   Permissions and access control

## Nested Structs and Mappings

Structs can include other structs, arrays, or mappings to create complex, hierarchical data models.

```jsx
struct Profile {
    string username;
    uint reputation;
}

struct Account {
    address owner;
    Profile profile;
}

struct Voter {
    bool registered;
    mapping(uint => bool) votes; // proposalId => voted
}

//Mappings inside structs can’t be returned directly from public functions due to storage limitations.

```

## Arrays : Ordered Collections

Arrays in Solidity store sequential data. They can be:

-   **Fixed-size:** Size defined at compile time.
-   **Dynamic:** Size can grow or shrink at runtime.

```jsx
uint[5] fixedArray;
uint[] public dynamicArray;

// Fixed-size arrays consume more gas and are less flexible.

```

**Array Operations**

-   `push()`: Adds an element to a dynamic array
-   `pop()`: Removes the last element
-   `length`: Returns current size
-   `delete`: Resets element to default

### Iterating Through Arrays and Mappings

**Arrays**

You can iterate over arrays using loops:

```jsx
for (uint i = 0; i < users.length; i++) {
    process(users[i]);
}

```

**Mappings**

Mappings are **not iterable**. To support iteration, maintain a parallel array of keys:

```jsx
mapping(address => uint) balances;
address[] public users;

function addBalance(address user, uint amount) public {
    if (balances[user] == 0) {
        users.push(user);
    }
    balances[user] += amount;
}

// Always consider gas implications when looping through large data sets.

```