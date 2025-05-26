# 6. Structs, Mappings & Arrays
> Build Your Pokédex – Catch, Store & Train Your Pokémon
Now that your Pokémon can fight and think, it’s time to organize them like a real Pokémon Master! . you’ll build your Pokédex and PC Storage System using powerful data structures: **structs**,**mappings**, and **arrays**.

## Structs : Define Your Pokémon Species

A struct is a user-defined data type that groups related variables into a single unit. Structs are useful for modeling entities such as user profiles, records, or metadata.
They are like the DNA of a Pokémon. You use them to define species, stats, evolution data, or even Trainer profiles.
```jsx
struct Pokemon {
    string name;
    string type;
    uint hp;
    uint level;
    bool legendary;
}
Pokemon public pikachu;

```


You can use structs to :
- Store each Pokémon’s profile
- Track battle stats
- Define evolution paths

Structs can be stored as:
-   **State variables** (persistent storage)
-   **Local variables** (in functions)
-   **Function parameters and return types**


## Mappings : Key-Value Storage

Mappings store key-value pairs and are commonly used for fast, efficient lookup.
They are like your Trainer Registry – they connect trainers to their Pokémon, badges, items, and more.

```jsx
mapping(address => Pokemon[]) public trainerToPokemon;


```

-   Keys can be of **value types** (e.g., `address`, `uint`, `bool`)
-   Values can be any type, including structs or arrays
-   **Mappings are not iterable**

Use Cases:

-   who owns the pokemon (`mapping(address => struct)`)
-   Ownership records
-   Permissions and access control

## Nested Structs and Mappings -Link Pokémon, Stats & Trainers

You can go deeper by nesting structs inside structs or combining with mappings for complex data like evolution chains or battle histories.

```jsx
struct BattleStats {
    uint wins;
    uint losses;
    mapping(address => bool) battled; // Tracks opponents
}

struct PokemonProfile {
    string name;
    string element;
    BattleStats stats;
}


//Mappings inside structs can’t be returned directly from public functions due to storage limitations.

```

## Arrays : Ordered Collections

Arrays in Solidity store sequential data. They can be:

-   **Fixed-size:** Size defined at compile time.
-   **Dynamic:** Size can grow or shrink at runtime.

```jsx
uint[5] fixedMyTeam;
Pokemon[] public DynamicMyTeam;

// Fixed-size arrays consume more gas and are less flexible.

```

**Array Operations**

-   `push()`: Adds an element to a dynamic array - Add a Pokémon to your team
-   `pop()`: Removes the last element - Release the last Pokémon
-   `length`: Returns current size - Total team size
-   `delete`: Resets element to default

### Iterating Through Arrays and Mappings

**Arrays**

You can iterate over arrays using loops:

```jsx
for (uint i = 0; i < myTeam.length; i++) {
    train(myTeam[i]);
}


```

**Mappings**

Mappings are **not iterable**. To support iteration, maintain a parallel array of keys:

```jsx
mapping(address => Pokemon[]) trainerToTeam;
address[] public trainers;

function registerTrainer(address trainer) public {
    if (trainerToTeam[trainer].length == 0) {
        trainers.push(trainer);
    }
}


// Always consider gas implications when looping through large data sets.

```


## 🧭 What’s Next?
Now that you’ve structured your world with Pokémon identities, stats, storage, and ownership logic, it’s time to open the Poké Mart and handle real-world value.

In the next module, you'll learn how to:
- Accept Ether from trainers
- Reward winners of Pokémon battles
- Set up secure in-game purchases (like buying Potions or Rare Candies)
- Manage payouts, security, and withdrawals in your smart contracts

